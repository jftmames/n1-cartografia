# Entorno de pruebas — Nivel 1 (Análisis por resultados)

Este documento define una configuración reproducible para ejecutar la batería A/B (7 categorías, 30 pares por categoría) y registrar resultados de forma trazable.

## 1. Estructura de repositorio
```
n1-cartografia/
  data/
    battery/            # dataset de prompts (CSV/JSONL)
    runs/               # salidas crudas por modelo/fecha
    annotations/        # anotaciones humanas (ciego)
  configs/
    run.yaml            # configuración de ejecución (modelos, seeds, temp…)
    rubric.yaml         # rúbricas de scoring (acierto, explicación, etc.)
  scripts/
    run_battery.py      # ejecuta prompts contra APIs
    normalize.py        # normaliza y versiona resultados
    score.py            # aplica scoring (humano/semiauto)
    analyze.py          # métricas + tablas
  prereg/
    hypotheses.md       # predicciones preregistradas
    analysis_plan.md    # outcomes y tests
  docs/
    README.md
    CHANGELOG.md
```

## 2. Requisitos mínimos (N1)
- Python 3.11+
- Acceso a APIs de modelos (OpenAI, Anthropic u otros)
- Librerías: `pandas`, `httpx` (o `requests`), `python-dotenv`, `tenacity`.
- Registro completo: exactitud, calibración, consistencia, self-consistency; logprobs solo si existen. (ver guía) 

## 3. Configuración estándar de ejecución
### 3.1 Parámetros por defecto
- `temperature`: 0.2 (modo “determinista”)
- `max_tokens`: 400
- `top_p`: 1.0
- `seed`: fijo por modelo (si la API lo soporta)
- `repetitions_self_consistency`: 5 (solo en fase SC, con temperature 0.7)

### 3.2 Bucle de modelos
Ejecutar **mínimo 4 modelos** (familias distintas si es posible) para testar estabilidad del patrón.

### 3.3 Control de reformulación (robustez)
Para cada prompt **B**:
- `B0`: original
- `B1`: paráfrasis
- `B2`: paráfrasis + distractor

(estos “variants” pueden añadirse en una iteración 2 sin romper preregistro, si se declara como ampliación)

## 4. Esquema de registro (run record)
Cada llamada guarda:
- `run_id`, `timestamp_utc`, `model`, `params` (temp, seed…)
- `prompt_id` (p.ej., CAT3_14_B)
- `prompt_text`
- `raw_response_text`
- `latency_ms`
- `finish_reason`
- `logprobs` (si aplica)
- `cost_estimate` (si la API lo expone)

## 5. Scoring y anotación (ciego)
- Anotadores **ciegos a modelo** y, si es viable, al tipo A/B.
- Variables:
  - `accuracy` (0/1 o escala si procede)
  - `confidence_expressed` (0–3)
  - `explanation_type` (a/b/c/d)
  - `robustness` (consistencia entre paráfrasis)
- Medir acuerdo (κ/α) y documentar discrepancias.

## 6. Outputs del análisis
- Tabla maestra: categoría × bin distribucional × modelo × Δ(A−B)
- Curvas por bin distribucional (A vs B)
- Informe preregistrado: qué predicciones se cumplieron y dónde aparecen fronteras.

## 7. Archivos generados en este paquete
- `N1_pairs_catalog_420.csv`
- `N1_pairs_catalog_420.jsonl`
