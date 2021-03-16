##### 1. Crear red para el cluster de hadoop

```
sudo docker network create --driver=bridge hadoop
```

##### 2. Inicializar el cluster

```
sudo ./start-container.sh
```

**output:**

```
start hadoop-master container...
start hadoop-slave1 container...
start hadoop-slave2 container...
root@hadoop-master:~# 
```
- Iniciar con 2  esclavos y un maestro
- Entraremos al contenedor master

##### 3. Iniciar hadoop

```
./start-hadoop.sh
```

##### 4. Un archivo txt de un libro

```
apt update && apt install curl -y 
curl --header 'Host: raw.githubusercontent.com' --user-agent 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:86.0) Gecko/20100101 Firefox/86.0' --header 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8' --header 'Accept-Language: en-US,en;q=0.5' --referer 'https://github.com/uracilo/english_books/blob/master/books/books.tar.gz' --header 'Upgrade-Insecure-Requests: 1' 'https://raw.githubusercontent.com/uracilo/english_books/master/books/books.tar.gz' --output 'books.tar.gz' 
```

##### 5. Crear un directorio

```
mv books.tar.gz input
mkdir input
```

##### 6. Revisar los tamaños de nuestros archivos

```
ls -flarts input
```
##### 7. Crear y mover  directorio input al DFS de  HADOOP

```
hdfs dfs -put input
```

##### 8. Revisar nuestro input directorio en HADOOP

```
hdfs dfs -ls  input
```

##### 9. ejecutar un trabajo en HADOOP

```
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/sources/hadoop-mapreduce-examples-2.7.2-sources.jar org.apache.hadoop.examples.WordCount input output
```

##### 10. ver el resultado del trabajo en HADOOP

```
hdfs dfs -cat output/part-r-00000
```

Inspirado en https://github.com/kiwenlau/hadoop-cluster-docker
