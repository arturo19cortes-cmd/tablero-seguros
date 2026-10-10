# Tablero de cartera de seguros

Aplicación de Streamlit para explorar una cartera de autos mediante filtros, indicadores, gráficas y un cotizador de prima empírica, prima GLM y precio al cliente.

Diplomado Machine Learning en Seguros · FC UNAM · Módulo 5 · Tema 1.

## Archivos del proyecto

| Archivo | Función |
| --- | --- |
| `app_streamlit.py` | Código del tablero proporcionado para la tarea. |
| `datos/datos.parquet` | Base proporcionada para la tarea, ya incluida. |
| `requirements.txt` | Las seis dependencias requeridas, fijadas en las versiones comprobadas. |
| `.gitignore` | Excluye la base local `cartera.db`, archivos temporales y secretos. |
| `README.md` | Instrucciones de ejecución y publicación. |

El archivo `cartera.db` se genera localmente a partir del Parquet. No debe subirse a GitHub.

## Ejecutar localmente

1. Abre esta carpeta en Visual Studio Code.
2. Comprueba que `datos/datos.parquet` está dentro de la carpeta extraída; ya se incluye en este paquete.
3. Selecciona un entorno de Python 3.12; si ya usas Anaconda, puedes activar tu entorno del diplomado.
4. Abre una terminal situada en la carpeta que contiene `app_streamlit.py` y ejecuta:

```bash
python -m pip install -r requirements.txt
python -m streamlit run app_streamlit.py
```

Abre la dirección local que muestre Streamlit. La primera carga ajusta los modelos y puede tardar más que las siguientes.

Para un entorno nuevo en Windows, opcionalmente puedes usar estos comandos en una terminal de tipo Command Prompt (CMD), antes de instalar las dependencias:

```bat
py -3.12 -m venv .venv
.venv\Scripts\activate.bat
```

## Subir a GitHub

1. Crea un repositorio nuevo llamado `tablero-seguros`, con visibilidad **Public**, como exige la tarea.
2. Déjalo vacío al crearlo: los archivos README y `.gitignore` ya están en esta carpeta.
3. En la terminal de esta carpeta, ejecuta lo siguiente. Sustituye `TU_USUARIO` por tu usuario real de GitHub antes de ejecutar la línea correspondiente:

```bash
git init
git add .
git status
git commit -m "Preparar tablero de seguros para deploy"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/tablero-seguros.git
git push -u origin main
```

Antes del commit, revisa en `git status` que se incluya `datos/datos.parquet` y que no se incluya `cartera.db`.

En GitHub, confirma que `app_streamlit.py` está en la raíz del repositorio y el Parquet dentro de `datos/`. Sube los archivos extraídos, no el ZIP.

## Publicar en Streamlit Community Cloud

1. Abre [Streamlit Community Cloud](https://share.streamlit.io/) e inicia sesión.
2. Selecciona **Create app** y la opción para desplegar una aplicación existente.
3. Completa estos campos:

| Campo | Valor |
| --- | --- |
| Repository | `TU_USUARIO/tablero-seguros` |
| Branch | `main` |
| Main file path | `app_streamlit.py` |
| Python version, en Advanced settings | `3.12` |

4. Pulsa **Deploy** y espera a que termine la carga.
5. Copia la URL asignada, con dominio `streamlit.app`.

Referencia: [documentación oficial de publicación de Streamlit](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/deploy).

## Comprobar antes de entregar

- Abre el enlace publicado en una ventana de incógnito y comprueba que carga sin errores.
- Cambia cobertura, sexo, uso, combustible y edad; pulsa **Aplicar filtros**.
- Confirma que aparecen exposición, número de siniestros, frecuencia, severidad y prima pura.
- Confirma que se muestran las gráficas de frecuencia y combined ratio.
- En **Cotizador**, selecciona un perfil y pulsa **Cotizar**.
- Revisa el orden de las tarjetas: **1 Empírico → 2 GLM → 3 Precio al cliente**.
- Para comprobar la prima empírica, utiliza un segmento con observaciones. Si una combinación no existe en la base, no hay una prima empírica estimable para ese segmento.
- Confirma que GitHub contiene el Parquet y no contiene `cartera.db`.

La entrega son **dos enlaces**: el tablero público funcionando y el repositorio público que lo despliega. Tener únicamente este proyecto descargado no completa la tarea.

## Si falta el Parquet al iniciar

El código original abre SQLite antes de intentar leer el Parquet. Si iniciaste sin el archivo, puede quedar una `cartera.db` vacía y aparecer después `no such table: cartera`.

En ese caso, detén Streamlit con Ctrl+C, coloca el Parquet en `datos/datos.parquet` y elimina únicamente la `cartera.db` generada dentro de esta carpeta. Ejecuta otra vez la aplicación para reconstruirla.

## Bonus opcional

La persistencia de cotizaciones en Google Sheets es un extra de hasta **0.10**. No se incluye en este paquete base. Para implementarla, sigue la Parte C de la guía del profesor y configura las credenciales con `st.secrets`.

## Alcance de esta preparación

`app_streamlit.py` es una copia íntegra de `app_streamlit_deploy.py`, con el nombre requerido por la tarea. El Parquet también se conserva íntegro.

Se verificó la aplicación con Python 3.12 y la base completa de 163,212 registros mediante AppTest de Streamlit: carga inicial, indicadores, filtros, selección vacía y recuperación, cotizador, valores límite de sus controles y recargos. Los indicadores y la prima empírica se cotejaron con cálculos realizados directamente sobre la base.

Para el perfil inicial (35 años, cobertura Amplia, Hombre, uso Particular, Diesel, vehículo de 5 años, potencia 70 y bonus 5), con gastos de 25% y margen de 5%, se obtuvieron estos resultados:

| Indicador | Resultado |
| --- | ---: |
| Pólizas del segmento empírico | 837 |
| 1. Prima pura empírica | $154.81 |
| 2. Prima pura GLM | $238.22 |
| 3. Prima de tarifa | $340.31 |

Referencia de la herramienta de verificación: [AppTest de Streamlit](https://docs.streamlit.io/develop/api-reference/app-testing/st.testing.v1.apptest).

Estas pruebas se realizaron en un entorno local de validación. **La publicación en tus cuentas de GitHub y Streamlit y la comprobación de la URL pública siguen pendientes.**
