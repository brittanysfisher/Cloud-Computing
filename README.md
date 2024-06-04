# Cloud-Computing

mkdir running-hadoop

cd running-hadoop

mkdir eu

mkdir wxw

ls

cd eu

git clone https://github.com/big-data-europe/docker-hadoop

cd docker-hadoop

touch AS_EU

ls

cd ..

cd ..

ls

cd wxw

git clone https://github.com/wxw-matt/docker-hadoop.git

cd docker-hadoop

touch AS_WXW

ls

docker run hello-world

ls docker-compose*

cp docker-compose.yml docker-compose-v1.yml

ls

cd ../../eu/docker-hadoop/

cp docker-compose.yml docker-compose-v1.yml

ls

docker ps

docker-compose up-d

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

head austen.txt

ls -al

wc austen.txt

** In separate terminal on local device **

cd running-hadoop/wxw/docker-hadoop/

ls

docker cp WordCount.jar namenode:/app/jars/



** Back to original terminal **

cd /

pwd

ls

ls app/jars

ls

hdfs dfs -ls /

hdfs dfs -mkdir /in-1

hdfs dfs -copyFromLocal -f /app/data/* /in-1

hdfs dfs -ls /in-1

ls

hadoop jar /app/jars/WordCount.jar WordCount /in-1 /out-1

hdfs dfs -head /out-1/part-r-00000

hdfs dfs -copyToLocal /out-1 /app/res/

head /app/res/out-1/part-r-00000

** Back to local device in separate terminal **

cd ../..

cd ../..

mkdir notes

cd notes

docker cp namenode:/app/res/out-1/part-r-00000 wordscounted.txt

ls

head wordscounted.txt
