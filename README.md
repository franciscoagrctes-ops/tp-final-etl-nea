# Pipeline Exportaciones del NEA

## Qué hace
Este pipeline ETL descarga datos de exportaciones de Chaco, Corrientes, Formosa y Misiones (1993–2024) desde la API de Series de Tiempo de datos.gob.ar (INDEC), los transforma en un dataset analítico único y los guarda en disco junto con una ficha técnica y un registro de cada corrida. Asimismo, combina dos fuentes: exportaciones por país de destino (dataset 357.1) y exportaciones por rubro (dataset 350.1), y las une para obtener, para cada fila (provincia, destino, año), el valor exportado, su participación relativa, la variación interanual, el ranking del destino ese año y el rubro principal de la provincia.

## Cómo instalarlo y ejecutarlo
1. Cloná el repositorio y entrá a la carpeta:

```
git clone https://github.com/franciscoagrctes-ops/tp-final-etl-nea.git
cd tp-final-etl-nea
```

2. Creá y activá el entorno virtual:

```
python -m venv .venv
.venv\Scripts\activate
```
3. Instalá las dependencias:

```
pip install -r requirements.txt
```

4. Corré el pipeline completo:

```
python src/main.py
```

## De dónde salen los datos

API de Series de Tiempo del portal de datos abiertos del Estado argentino (datos.gob.ar), con datos del INDEC. No requiere credenciales. Documentación: https://datosgobar.github.io/series-tiempo-ar-api/

## Qué encontré en los datos

Un caso llamativo aparece en Corrientes en 2020: las exportaciones a Brasil saltaron a 399.14 millones de USD, un 1478% más que el año anterior, y pasaron a representar el 68% de todo lo exportado por la provincia ese año (el rubro principal fue combustibles y energía). Es un salto atípico incluso para un vínculo comercial tan fuerte como el de Corrientes con Brasil, y coincide con el primer año de la pandemia, probablemente refleje un cambio puntual en la demanda energética regional más que una tendencia sostenida.

## Salidas del pipeline

- data/processed/exportaciones_nea.csv: dataset final (13 columnas, ~1408 filas)
- data/processed/resumen.json: ficha técnica de la corrida
- logs/pipeline.log: una línea de registro por cada ejecución