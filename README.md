# Proyecto 1 — Bodega de datos, ETL y Análisis Descriptivo

**Dataset:** *Presuntos Homicidios. Colombia, 2015 a 2024. Cifras definitivas* (Medicina Legal, datos.gov.co) — 125.284 registros × 33 columnas.

**Pregunta guía:** ¿Cuáles son los patrones temporales, geográficos y operacionales de los homicidios en Colombia que permiten identificar zonas de alto riesgo y factores para la prevención del delito?

**Integrantes:** Alejandra Osorio Giraldo (2266128) · Sebastián Barco (2380599) · Santiago Montoya (2380372) · Laura Rivera (2380712)

> Los integrantes se comprometen a mantener el dataset elegido durante los tres proyectos del semestre (P1, P2/3, P4). Cambios solo por autorización del profesor.

## Cómo correr el proyecto

1. **Requisitos:** Python 3.10+ y PostgreSQL 14+ en ejecución.
2. **Clonar e instalar dependencias**
   ```bash
   git clone https://github.com/XEBAX10/PROYEC-1-CIencia_Datos.git
   cd PROYEC-1-CIencia_Datos
   pip install -r requirements.txt
   ```
3. **Crear la base de datos vacía** (una sola vez):
   ```bash
   psql -U postgres -c "CREATE DATABASE homicidios;"
   ```
4. **Configurar credenciales:** copiar `.env.example` como `.env` y ajustar `DATABASE_URL`
   ```
   DATABASE_URL=postgresql+psycopg2://postgres:tu_contraseña@localhost:5432/homicidios
   ```
5. **Ejecutar los notebooks en orden** (en cada uno: *Kernel → Restart & Run All*):
   1. `entrega/fase_b_etl.ipynb` — extrae el CSV crudo, lo transforma y carga la bodega en PostgreSQL.
   2. `entrega/fase_c_sql.ipynb` — 6 consultas SQL analíticas.
   3. `entrega/fase_d_visualizaciones.ipynb` — 8 visualizaciones (se guardan en `entrega/figuras/`).

## Estructura

```
├── Presuntos_Homicidios..._20260916.csv   ← CSV crudo (fuente)
├── entrega/
│   ├── fase_a_diseño.pdf           ← modelo estrella + justificación
│   ├── diagrama_bodega.png
│   ├── fase_b_etl.ipynb
│   ├── fase_c_sql.ipynb
│   ├── fase_d_visualizaciones.ipynb
│   ├── informe.pdf
│   └── figuras/                    ← PNG de las 8 visualizaciones
├── docs/diagrama_bodega.dbml       ← fuente del diagrama (dbdiagram.io)
├── .env.example
└── requirements.txt
```

## Modelo

Esquema estrella: `fact_homicidios` (grano = una víctima) + `dim_tiempo`, `dim_geografia`, `dim_victima`, `dim_modalidad`. Detalle en `entrega/fase_a_diseño.pdf`.
