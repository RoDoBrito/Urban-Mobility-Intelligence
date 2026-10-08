# Project Notes
## Data Quality Audit

### Dataset
- Archivo analizado: Yellow Taxi Trip Records - July 2026
- Filas: 3,530,109
- Columnas: 21
- Formato: Parquet
- Row groups: 4

### Missing values

Se detectó un patrón estructurado de valores faltantes.

Las siguientes columnas contienen 969,727 valores nulos (27.47%):

- passenger_count
- RatecodeID
- store_and_fwd_flag
- congestion_surcharge
- Airport_fee

Los valores faltantes aparecen simultáneamente en las mismas 969,727 filas.

Al comparar estos registros con payment_type, se observó que el 100% tiene:

- payment_type = 0

Según la documentación de NYC TLC, payment_type = 0 corresponde a Flex Fare trips.

Además, 969,417 de estos 969,727 registros contienen información en request_source.

### Decision

No eliminar estos registros mediante dropna().

Los valores faltantes presentan un patrón asociado a los viajes Flex Fare y no deben considerarse automáticamente errores de calidad.

La columna request_source se conservará para análisis posterior.