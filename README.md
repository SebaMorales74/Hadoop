# Hadoop / Docker-Compose by @Juliopez
## Contexto
Este repositorio asume que eres parte del curso de Big Data P2024 en Inacap sede Renca.
Y que estás haciendo los pasos basado en [Este video](https://www.youtube.com/watch?v=qjjBWUUJq3s)

## Requerimientos
Primero debes de instalar docker en tu maquina ubuntu linux:
```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Finalmente, vamos a probar que docker funciona correctamente.
```sh
sudo docker run hello-world
```
Vamos a instalar git y clonar el repositorio con los siguientes 3 comandos:
```sh
sudo apt-get install git
```
```sh
git --version
```
```sh
git clone https://github.com/SebaMorales74/Hadoop.git
```

Ingresamos a la carpeta cambiado de directorio con:
```sh
cd ./Hadoop
```

Ahora, debes de componer los contenedores con el siguiente comando:
```sh
sudo docker compose up -d
```

Para probar que los contenedores están arriba puedes utilizar:
```sh
sudo docker compose ps -a
```

Listo. Ahora puedes utilizar este repositorio :D

## Infraestructura Big Data usando docker-compose.
<br> En este contendeor podras encontrar HDFS, Hive, Spark, Hue, Zeppelin, Kafka, Zookeeper y NiFi
<br> Para la implementacion de este contenedor solo basta con descargar (clonar) este repositorio y, proceder a descomprimir en tu maquina local. 
<br> Luego, desde la linea de comando, ubicate sobre el directorio Hadoop y ejecuta `docker-compose up`
<br>Con esto completamos la instalación de Hadoop – HDFS -Spark -Hive- NiFi.
## Podemos comprobar la correcta ejecución de la siguiente forma. 
<br>En un browser ingresar a http://localhost: `numero de puerto`
<br>Donde <b>numero de puerto</b> puede ser:
<br>** 50070 (visualiza Hadoop y sus namenode)
<br>** 8080 (Spark Master)
<br>** 8081 (Spark  Worker)
<br>** 8888 (Hue. Se solicitará la creación de una cuenta. Ingrese admin como usuario y admin como password)
<br>** 9999 (NiFi)
<br>** 3030 (kafka)
<br>** 18630 (StreamSets. Utilice admin / admin)
<br>** 19090 (zeppelin)
### Para el uso de Hive 
<br> Ejecute en la consola `sudo docker exec -it hive-server bash`
<br> Luego ingrese al directorio donde esta alojado Hive, para esto deberá ejecutar el comando `cd /opt/hive/bin`
<br> Una vez dentro de dicho directorio, ejecute Hive con el siguiente comando  `./hive`
### Para el uso de mysql 
<br> Ejecute en la consola `sudo docker exec -it database bash`
<br> Luego el comando `mysql -h localhost -u root -p`
<br> Posterior a esto se solicitara la contraseña, la cual es : `secret`
### Para el uso de Spark (Scala)
<br> Ejecute en la consola `sudo docker exec -it spark-master bash`
<br> Luego ingrese al directorio donde esta alojado Spark, para esto deberá ejecutar el comando `cd /spark/bin`
<br> Una vez dentro de dicho directorio, ejecute Hive el siguiente comando  `./spark-shell`
### Para el uso de pyspark (Python)
<br> Ejecute en la consola `sudo docker exec -it spark-master bash`
<br> Luego ingrese al directorio donde esta alojado Spark, para esto deberá ejecutar el comando `cd /spark/bin`
<br> Una vez dentro de dicho directorio, ejecute el siguiente comando  `./pyspark`
### Para el uso de Kafka
<br> Ejecute en la consola `sudo docker exec -it kafka bash`
<br> Luego ingrese al directorio donde esta el productos y consumidor de Kafka, para esto deberá ejecutar el comando `cd /usr/local/bin`
<br> Para crear un TOPIC: `./kafka-topics  --create --zookeeper 172.27.1.15:2181 --replication-factor 1 --partitions 1 --topic EJEMPLO`
<br> Para verificar la creacion: `./kafka-topics --list --zookeeper 172.27.1.15:2181`
<br> Para crear un PRODUCTOR: `./kafka-console-producer --broker-list localhost:9092 --topic EJEMPLO`
<br> Para crear un CONSUMIDOR: `./kafka-console-consumer --bootstrap-server localhost:9092 --from-beginning --topic EJEMPLO`
<br>
<br>
<br> SI tienes problemas con HUE, mira la solucion propuesta aqui: [https://youtu.be/Ck4sRPa0o24](https://youtu.be/Ck4sRPa0o24)
<br>
<br> Si necesitas trabajar con sqoop, aqui una propuesta: [https://youtu.be/hLJFzOAbY8Q](https://youtu.be/hLJFzOAbY8Q)
<br>
<br> Mas info en [Blog de Julio Lopez-Nunez](https://juliopezblog.wordpress.com/).
