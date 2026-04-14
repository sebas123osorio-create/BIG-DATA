Descripción 
Esta solución de Big Data implementa un sistema híbrido de procesamiento para el análisis de calidad del aire en Risaralda y Bogotá, utilizando Apache Spark para la limpieza y análisis exploratorio (EDA) de datos históricos mediante transformaciones de DataFrames, e integrando Apache Kafka como broker de mensajería para la ingesta de flujos en tiempo real. La arquitectura permite normalizar registros críticos de contaminación (PM10), calcular promedios por estación de monitoreo y visualizar métricas en vivo con una tasa de entrada de 1.5 reg/seg y un consumo optimizado de memoria de 80 KB, garantizando una herramienta escalable para la toma de decisiones ambientales inmediatas.

Instrucciones para la Ejecución

1. Requisitos Previos
Tener instalado Java JDK 8 o 11, Apache Spark y Apache Kafka en la máquina virtual o entorno local.

Instalar la dependencia necesaria para la comunicación entre Python y Kafka:

comando:

pip install kafka-python


2. Ejecución de Procesamiento Batch
Asegúrese de que el archivo calidad_aire_bogota.csv esté en la misma carpeta que el script.

Ejecute el script de análisis histórico:

comando:

python batch_analisis.py

3. Ejecución de Procesamiento en Tiempo Real
Siga este orden estricto abriendo terminales independientes:

Paso 1 (Servidores): Inicie Zookeeper y posteriormente el servidor de Kafka.

Paso 2 (Canal): Cree el topic de comunicación:

comando:

.\bin\windows\kafka-topics.bat --create --topic calidad_aire_topic --bootstrap-server localhost:9092

Paso 3 (Emisor): Ejecute el generador de datos (Productor):

comando:

python productor_unad.py

Paso 4 (Receptor): Ejecute la aplicación de Spark Streaming:

comando:

spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0 stre