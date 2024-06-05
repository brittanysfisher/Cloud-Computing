# Cloud-Computing - Running Hadoop

1. Make a working directory
```
mkdir running-hadoop
cd running-hadoop
```

2. Make a working directory inside previous directory, for each repository - EU and WXW. Then cd into EU directory
```
mkdir eu
mkdir wxw
cd eu
```

3. Clone EU repository inside EU directory, then create EU label inside docker-hadoop directory.
```
git clone https://github.com/big-data-europe/docker-hadoop
cd docker-hadoop
touch AS_EU
```
4. Move back to running-hadoop directory, and cd into WXW. Once there, clone the WXW repository. Then cd into docker-hadoop and create WXW label with touch.
```
cd ..
cd ..
ls
cd wxw
git clone https://github.com/wxw-matt/docker-hadoop.git
cd docker-hadoop
touch AS_WXW
```
5. After running docker desktop, test to make sure it is working.
```
docker run hello-world
```
6. Check all docker-compose files available with *
```
ls docker-compose*
```
7. Copy docker-compose.yml as docker-compose-v1.yml in both WXW and EU directories.
```
cp docker-compose.yml docker-compose-v1.yml
ls
cd ../../eu/docker-hadoop/
cp docker-compose.yml docker-compose-v1.yml
ls
```
8. Bring up the hadoop container
```
docker-compose up-d
```
10. Use docker ps to list the nodes and identify the name node
```
docker ps
```
11. Move into namenode
```
docker exec -it namenode /bin/bash
```
12. Test hello world to make sure everything is correct
```
echo hello world
```
13. Make designated directories inside the node
```
mkdir app
mkdir app/data
mkdir app/res
mkdir app/jars
```
14. Move into app/data directory and obtain files using curl
```
cd /app/data
curl https://www.gutenberg.org/cache/epub/1342/pg1342.txt -o austen.txt
curl https://www.gutenberg.org/cache/epub/84/pg84.txt -o shelley.txt
curl https://www.gutenberg.org/cache/epub/768/pg768.txt -o bronte.txt
```
15. Test that curl worked
```
head austen.txt
ls -al
wc austen.txt
```

** In separate terminal on local device **
16. Move into appropriate directory listed below, copy the WordCount.jar from the wxw diretory, and copy it into the namenode app/jars directory.
```
cd running-hadoop/wxw/docker-hadoop/
ls
docker cp WordCount.jar namenode:/app/jars/
```

** Back to original terminal **
17. Move back to the top directory and load data in HDFS
```
cd /
pwd
ls app/jars
hdfs dfs -ls /
hdfs dfs -mkdir /in-1
```
18. Copy the results out of HDFS to local device
```
hdfs dfs -copyFromLocal -f /app/data/* /in-1
hdfs dfs -ls /in-1
ls
hadoop jar /app/jars/WordCount.jar WordCount /in-1 /out-1
```
19. See the results
```
hdfs dfs -head /out-1/part-r-00000
hdfs dfs -copyToLocal /out-1 /app/res/
head /app/res/out-1/part-r-00000
```

** Back to local device in separate terminal **
20. cd to desired directory in local device and make a new "notes" directory. Copy the results from previous step to notes directory.
```
cd ../..
cd ../..
mkdir notes
cd notes
docker cp namenode:/app/res/out-1/part-r-00000 wordscounted.txt
ls
head wordscounted.txt
```
