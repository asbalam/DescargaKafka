# APACHE KAFKA: Introducción, descarga y prueba en Windows

Apache Kafka es una plataforma de mensajería y transmisión de eventos diseñada para el procesamiento en tiempo real de flujos de datos. Permite la ingesta, almacenamiento y distribución de datos entre múltiples aplicaciones o sistemas. Algunas características clave de Kafka incluyen su modelo de publicación-suscripción, capacidad de procesamiento de datos en tiempo real, y su utilidad en diversos casos de uso como la ingesta de datos, la integración de sistemas y la arquitectura de microservicios.

## Descarga en Windows

Accede al siguiente enlace para descargar Apache Kafka: [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)
Selecciona la versión deseada y descarga el archivo "kafka_<versión>.tgz"
Descomprime el archivo descargado y mueve la carpeta resultante a la ubicación deseada en tu sistema, por ejemplo, "C:/kafka".

## Configuración

1. Abre la carpeta "C:/kafka/config" y encuentra el archivo "server.properties".
2. Edita el archivo "server.properties" y cambia la configuración "log.dirs=/tmp/kafka-logs" a "log.dirs=c:/kafka/kafka-logs".
3. Abre la carpeta "C:/kafka/config" y encuentra el archivo "zookeeper.properties".
4. Edita el archivo "zookeeper.properties" y cambia la configuración "dataDir=/tmp/zookeeper" a "dataDir=c:/kafka/zookeeper".

## Iniciar ZooKeeper y el Servidor Kafka

1. Abre una ventana de comandos en la ubicación "C:/kafka".
2. Ejecuta el siguiente comando para iniciar ZooKeeper: `.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties`.
3. Abre otra ventana de comandos en la ubicación "C:/kafka".
4. Ejecuta el siguiente comando para iniciar el servidor Kafka: `.\bin\windows\kafka-server-start.bat .\config\server.properties`.

## Crear un Topic y probar la transmisión de datos

1. En la ventana de comandos del servidor Kafka, ejecuta el siguiente comando para crear un nuevo Topic llamado "test": <br>
`bin/windows/kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test`.

2. En la ventana de comandos del productor, ejecuta el siguiente comando para comenzar a producir mensajes en el Topic "test": <br>
`bin/windows/kafka-console-producer.bat --broker-list localhost:9092 --topic test`.
  
3. En la ventana de comandos del consumidor, ejecuta el siguiente comando para consumir los mensajes del Topic "test": <br>
`bin/windows/kafka-console-consumer.bat --topic test --bootstrap-server localhost:9092 --from-beginning`.

4. Prueba enviando mensajes desde el productor y verifica que se reflejen en la ventana del consumidor. <br>

5. Para ver clave de mensaje en el consumidor<br>
`bin/windows/kafka-console-consumer.bat --topic test --bootstrap-server localhost:9092 --property print.key=true`

6. Para agregar clave al mensaje en el productor  <br>
`bin/windows/kafka-console-producer.bat --broker-list localhost:9092 --topic test --property "parse.key=true" --property "key.separator=:"` <br>
Ejemplo de mensaje a enviar
`este es mi clave: este es mi mensaje`

##Kafka con 2 brokers
Creacion de otro servidor
Copiar `server.properties`

Ejemplo de copiado
`cp server.properties server1.properties`

Modificar parametro basicos, por ejemplo
broker.id=1
listeners=PLAINTEXT://localhost:9093
advertised.listeners=PLAINTEXT://localhost:9093

Ejecutar servidor de kafka `.\bin\windows\kafka-server-start.bat .\config\server.properties`

Creacion de topics con mas de una replica
bin/windows/kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 2 --partitions 8 --topic testX2

Revisar las propiedades de una replica
bin/windows/kafka-topics.bat --describe --bootstrap-server localhost:9092 --topic testX2


##Lista de mas comandos
Lista de topics <br>
`bin/windows/kafka-topics.bat --list --bootstrap-server localhost:9092`. <br>
Eliminar topic <br>
`bin/windows/kafka-topics.bat --delete --bootstrap-server localhost:9092 --topic nombre_del_tema`. <br>
Ver describción del topic<br>
`bin/windows/kafka-topics.bat --describe --bootstrap-server localhost:9092 --topic nombre_del_tema`.


En resumen, Apache Kafka es una potente plataforma de mensajería y transmisión de eventos que permite el procesamiento en tiempo real de flujos de datos. Con su modelo de publicación-suscripción y su capacidad para gestionar flujos masivos de datos, Kafka es una herramienta versátil utilizada en diversos sectores para la transmisión de eventos en tiempo real, integración de sistemas y arquitecturas basadas en eventos.

`bin/windows/kafka-topics.bat --describe --bootstrap-server localhost:9092 --topic nombre_del_tema`.


En resumen, Apache Kafka es una potente plataforma de mensajería y transmisión de eventos que permite el procesamiento en tiempo real de flujos de datos. Con su modelo de publicación-suscripción y su capacidad para gestionar flujos masivos de datos, Kafka es una herramienta versátil utilizada en diversos sectores para la transmisión de eventos en tiempo real, integración de sistemas y arquitecturas basadas en eventos.
