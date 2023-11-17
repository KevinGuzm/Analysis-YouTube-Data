# YouTube Data Analysis Project with AWS

This project utilizes a variety of technologies and services to gather, store, and analyze data from YouTube channels. Here's a detailed workflow of the project:

## Data Collection

The **YouTube API** was used to fetch data from certain YouTube channels. For each channel, the following statistics were gathered:

- Total views
- Number of subscribers
- Video count

These data were collected using a custom Python function called `get_stats`, which takes an API key and a channel ID as parameters.

## Data Processing and Storage

The gathered data were processed using **AWS Lambda** and **EventBridge**. A Lambda function was created that triggers in response to a specific event. This function performs the following tasks:

1. Retrieves a CSV file from an S3 bucket that contains the IDs of the YouTube channels.
2. Uses the `channels_stats` function to gather the statistics for each channel.
3. Saves the results in a new CSV file.
4. Uploads the CSV file to an S3 bucket.

The code for this Lambda function is located in the `lambda_handler.py` file.

## Data Analysis

Once the data are stored in S3, **Amazon Athena** and **Amazon Glue** are used to analyze them. Amazon Glue is used to catalog the data and make them available for queries, while Amazon Athena allows SQL queries to be performed on the stored data.

Several SQL queries were performed to analyze the statistics of the YouTube channels. These queries provide valuable insights into the growth and performance of the channels over time.

## SQL Queries

The SQL queries that were performed are as follows:

1. **Query 1**: This query selects all data from the "youtube_stats_demo" table in the "channel_stats" schema where the channel name is 'PeladoNerd'.

2. **Query 2**: This query creates a temporary table named `STATS` that includes a row for each record of the 'Fazt_web' channel, along with the previous record's `subscribers`, `video_count`, and `total_views`. It then selects the `channel_name`, `total_views`, `prev_viewsc`, and calculates the percentage change in views between the current and previous record.

3. **Final Query**: This query is similar to Query 2 but also calculates the change in `subscribers` and `video_count` in addition to `total_views`. It provides the absolute change (`qty_susc`, `qty_videos`, `qty_views`) and the percentage growth (`grow_susc`, `grow_videos`, `grow_views`) for each of these metrics.

These queries can provide valuable insights into the growth and performance of the YouTube channel 'Fazt_web' over time.

## Summary

This project demonstrates how various technologies and services can be used to gather, process, store, and analyze large amounts of data efficiently. Although this project focused on YouTube data, the workflow could easily be adapted to work with other types of data and data sources.

=======================================================
# Proyecto de Análisis de Datos de YouTube con AWS

Este proyecto utiliza una variedad de tecnologías y servicios para recopilar, almacenar y analizar datos de canales de YouTube. A continuación, se detalla el flujo de trabajo del proyecto:

## Recopilación de datos

Se utilizó la **API de YouTube** para obtener datos de ciertos canales de YouTube. Para cada canal, se recopilaron las siguientes estadísticas:

- Total de vistas
- Número de suscriptores
- Recuento de videos

Estos datos se recopilaron utilizando una función personalizada de Python llamada `get_stats`, que toma como parámetros una clave de API y un ID de canal.

## Procesamiento y almacenamiento de datos

Los datos recopilados se procesaron utilizando **AWS Lambda** y **EventBridge**. Se creó una función Lambda que se activa en respuesta a un evento específico. Esta función realiza las siguientes tareas:

1. Recupera un archivo CSV de un bucket de S3 que contiene los ID de los canales de YouTube.
2. Utiliza la función `channels_stats` para recopilar las estadísticas de cada canal.
3. Guarda los resultados en un nuevo archivo CSV.
4. Carga el archivo CSV a un bucket de S3.

El código para esta función Lambda se encuentra en el archivo `lambda_handler.py`.

## Análisis de datos

Una vez que los datos están almacenados en S3, se utilizan **Amazon Athena** y **Amazon Glue** para analizarlos. Amazon Glue se utiliza para catalogar los datos y hacerlos disponibles para consultas, mientras que Amazon Athena permite realizar consultas SQL en los datos almacenados.

Se realizaron varias consultas SQL para analizar las estadísticas de los canales de YouTube. Estas consultas proporcionan información valiosa sobre el crecimiento y rendimiento de los canales a lo largo del tiempo.

## Consultas SQL

Las consultas SQL que se realizaron son las siguientes:

1. **Consulta 1**: Esta consulta selecciona todos los datos de la tabla "youtube_stats_demo" en el esquema "channel_stats" donde el nombre del canal es 'PeladoNerd'.

2. **Consulta 2**: Esta consulta crea una tabla temporal llamada `STATS` que incluye una fila para cada registro del canal 'Fazt_web', junto con el registro anterior de `subscribers`, `video_count`, y `total_views`. Luego selecciona el `channel_name`, `total_views`, `prev_viewsc`, y calcula el cambio porcentual en vistas entre el registro actual y el anterior.

3. **Consulta Final**: Esta consulta es similar a la Consulta 2 pero también calcula el cambio en `subscribers` y `video_count` además de `total_views`. Proporciona el cambio absoluto (`qty_susc`, `qty_videos`, `qty_views`) y el crecimiento porcentual (`grow_susc`, `grow_videos`, `grow_views`) para cada una de estas métricas.

Estas consultas pueden proporcionar valiosos conocimientos sobre el crecimiento y rendimiento del canal de YouTube 'Fazt_web' a lo largo del tiempo.

## Resumen

Este proyecto demuestra cómo se pueden utilizar diversas tecnologías y servicios para recopilar, procesar, almacenar y analizar grandes cantidades de datos de manera eficiente. Aunque este proyecto se centró en los datos de YouTube, el flujo de trabajo podría adaptarse fácilmente para trabajar con otros tipos de datos y fuentes de datos.
