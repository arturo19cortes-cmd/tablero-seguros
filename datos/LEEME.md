# Datos de la aplicación

Esta carpeta incluye el archivo `datos.parquet` proporcionado para la tarea.

Conserva su ubicación: `datos/datos.parquet`, relativa a la raíz del repositorio.
La base contiene 163,212 registros y 18 columnas. Se incluyó íntegra, sin modificar sus datos.

El código utiliza estas columnas originales:

- `edad_conductor`
- `antiguedad_vehiculo`
- `potencia`
- `nivel_bonus`
- `cobertura`
- `sexo`
- `uso`
- `combustible`
- `exposicion`
- `num_siniestros`
- `severidad`
- `monto_total`

La exposición es positiva en todos los registros. La severidad está ausente en las pólizas sin siniestros; el modelo de severidad utiliza únicamente registros con siniestros.
