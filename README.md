# Proyectos 2 y 3 — Análisis, Limpieza y Modelado: Presuntos homicidios en Colombia (2015–2024)

**Dataset:** *Presuntos Homicidios. Colombia, 2015 a 2024. Cifras definitivas* (Medicina Legal, datos.gov.co) — 125.284 registros × 33 columnas. Es el mismo dataset del Proyecto 1.

**Pregunta de negocio:** ¿se puede anticipar, con las características de la víctima, el lugar y el momento del hecho, si un homicidio será cometido con **arma de fuego**? ¿Qué perfiles de municipios existen según su patrón de violencia?

**Integrantes:** Alejandra Osorio Giraldo (2266128) · Sebastián Barco (2380599) · Santiago Montoya (2380372) · Laura Rivera (2380712)

## Resultados principales

| Modelo | Accuracy | F1 | ROC-AUC |
|---|---|---|---|
| Regresión Logística | 0,669 | 0,753 | 0,716 |
| Árbol de Decisión | 0,683 | 0,773 | 0,689 |
| **Random Forest (elegido)** | **0,698** | **0,782** | **0,732** |

K-Means (k = 4) sobre 464 municipios: Silhouette 0,219 · Davies-Bouldin 1,40.

## Cómo correr el proyecto

1. **Requisitos:** Python 3.10 a 3.12.
2. **Clonar e instalar dependencias**
   ```bash
   git clone https://github.com/XEBAX10/PROYEC-1-CIencia_Datos.git
   cd PROYEC-1-CIencia_Datos
   pip install -r requirements.txt
   ```
3. **Verificar el CSV fuente** en la raíz del repositorio: `Presuntos_Homicidios._Colombia,_2015_a_2024._Cifras_definitivas_20260916.csv`.
4. **Ejecutar los notebooks en orden**, abriéndolos desde la carpeta `entrega/` (en cada uno: *Kernel → Restart & Run All*):
   1. `entrega/fase_a_eda.ipynb` — análisis exploratorio (histogramas, boxplots, Pearson/Spearman, violín, Pareto).
   2. `entrega/fase_b_limpieza.ipynb` — limpieza y normalización; genera `entrega/datos_limpios.parquet`.
   3. `entrega/fase_c_modelos.ipynb` — 3 modelos supervisados + K-Means; lee el parquet de la Fase B.

   Las figuras se guardan en `entrega/figuras/`.

> Los Proyectos 2 y 3 **no necesitan PostgreSQL**. El `.env.example` y los notebooks `fase_b_etl`, `fase_c_sql` y `fase_d_visualizaciones` son del Proyecto 1.

## Estructura

```
├── Presuntos_Homicidios..._20260916.csv   ← CSV crudo (fuente)
├── entrega/
│   ├── fase_a_eda.ipynb                   ← Fase A: análisis exploratorio
│   ├── fase_a_hallazgos.pdf               ← 3 hallazgos principales
│   ├── fase_b_limpieza.ipynb              ← Fase B: limpieza y normalización
│   ├── fase_b_justificacion.pdf           ← pasos y justificación de cada decisión
│   ├── datos_limpios.parquet              ← salida de la Fase B (124.914 × 108)
│   ├── fase_c_modelos.ipynb               ← Fase C: modelos supervisados y clustering
│   ├── fase_c_analisis_modelos.pdf        ← tabla comparativa y modelo elegido
│   ├── metricas_modelos.csv
│   ├── informe_p2p3.pdf                   ← Fase D: informe final
│   ├── presentacion.pdf                   ← Fase D: presentación
│   └── figuras/                           ← PNG de todas las visualizaciones
├── .env.example                           ← (Proyecto 1) conexión a PostgreSQL
├── requirements.txt
└── README.md
```

## Proyecto 1 (entregado)

Bodega dimensional (esquema estrella) en PostgreSQL, ETL y 6 consultas SQL: `entrega/fase_b_etl.ipynb`, `entrega/fase_c_sql.ipynb`, `entrega/fase_d_visualizaciones.ipynb`, `entrega/informe.pdf` y `entrega/fase_a_diseño.pdf`. Para correrlos se necesita PostgreSQL 14+ y un `.env` creado a partir de `.env.example`.
