# Cloud-Computing

git clone https://github.com/big-data-europe/docker-hadoop
cd docker-hadoop

ls

docker-compose up-d

docker run hello-world

docker ps

docker exec -it namenode /bin/bash

echo hello world

mkdir app
mkdir app/data
mkdir app/res
mkdir app/jars

cd /app/data
curl https://www.gutenberg.org/cache/epub/1342/pg1342.txt -o austen.txt
curl https://www.gutenberg.org/cache/epub/84/pg84.txt -o shelley.txt
curl https://www.gutenberg.org/cache/epub/768/pg768.txt -o bronte.txt

ls -al

docker cp .\jobs\jars\WordCount.jar namenode:/app/jars/WordCount.jar

hdfs dfs -mkdir /test-1-input
hdfs dfs -copyFromLocal -f /app/data/*.txt /test-1-input/
hdfs dfs -ls /test-1-input

hadoop jar /app/jars/WordCounter.jar WordCounter /test-1-input /test-1-output

jar jars/WordCounter.jar WordCounter
