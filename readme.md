## Hive and Hadoop compatible versions
https://docs.qubole.com/en/latest/user-guide/engines/hive/use-hive-versions.html

## Install Hadoop 3.2.4
https://www.youtube.com/watch?v=Slbi-uzPtnw
<br>
https://codewitharjun.medium.com/install-hadoop-on-ubuntu-operating-system-6e0ca4ef9689


## Install Hive 3.1.2
https://www.youtube.com/watch?v=wPIawRML168


**Steps for hive installation**
-	Download and Unzip Hive
-	Edit .bashrc file
-	Edit hive-config.sh file
-	Create Hive directories in HDFS
-	Initiate Derby database
-	Configure hive-site.xml file

**download and unzip Hive**

```
wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
tar xzf apache-hive-3.1.2-bin.tar.gz
```

**Edit .bashrc file**

```
sudo nano .bashrc
export HIVE_HOME= /home/hdoop/apache-hive-3.1.2-bin

export PATH=$PATH:$HIVE_HOME/bin
source ~/.bashrc
```

**Edit hive-config.sh file**

```
sudo nano $HIVE_HOME/bin/hive-config.sh
export HADOOP_HOME=/home/hdoop/hadoop-3.2.1
```

**Create Hive directories in HDFS**

```
hdfs dfs -mkdir /tmp
hdfs dfs -chmod g+w /tmp
hdfs dfs -mkdir -p /user/hive/warehouse
hdfs dfs -chmod g+w /user/hive/warehouse
```

**Fixing guava problem – Additional step**
```
rm $HIVE_HOME/lib/guava-19.0.jar
cp $HADOOP_HOME/share/hadoop/hdfs/lib/guava-27.0-jre.jar $HIVE_HOME/lib/
```

**Initialize Derby and hive**
```
schematool -initSchema -dbType derby
hive
```

**optional Step – Edit hive-site.xml**

```
cd $HIVE_HOME/conf
cp hive-default.xml.template hive-site.xml
sudo nano hive-site.xml – change metastore location to above created hdfs path(/user/hive/warehouse)
```
