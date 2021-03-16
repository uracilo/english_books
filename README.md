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
wget https://github.com/uracilo/english_books/blob/master/books/books.tar.gz   
```

##### 5. Crear un directorio

```
mkdir input
```

##### 6. Revisar los tamaños de nuestros archivos

```
ls -flarts input
```
##### 7. Crear y mover  directorio input al DFS de  HADOOP

```
hdfs dfs -mkdir -p test
hdfs dfs -put input
```

##### 8. Revisar nuestro input directorio en HADOOP

```
hdfs dfs –ls  input
```

##### 9. Leer las primeras lineas de nuestro archivo en HADOOP

```
hdfs dfs -cat  input/odisea.tar.gz | zcat | tail -n 20
```

##### 10. Eliminar el archivo en HADOOP

```
hdfs dfs –rm –f /user/rawdata/example/odisea.tar.gz
```

##### 11. ejecutar un trabajo en HADOOP

```
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/sources/hadoop-mapreduce-examples-2.7.2-sources.jar org.apache.hadoop.examples.WordCount input output
```

##### 12. ver el resultado del trabajo en HADOOP

```
hdfs dfs -cat output/part-r-00000
```


Inspirado en https://github.com/kiwenlau/hadoop-cluster-docker
