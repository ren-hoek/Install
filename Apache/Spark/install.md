mkdir Install/Apache/Spark

download and install latest scala
cd Install/Apache/Spark
wget http://downloads.lightbend.com/scala/2.12.1/scala-2.12.1.tgz
sudo tar -xvf scala-2.12.1.tgz -C /opt
mv /opt/scala-2.12.1.tgz /opt/scala
sudo adduser scala --home /opt/scala
sudo chown -R scala:scala /opt/scala
sudo chmod -R 775 /opt/scala

download and install latest spark
wget http://www-eu.apache.org/dist/spark/spark-2.1.0/spark-2.1.0-bin-hadoop2.7.tgz

verify download
wget http://www-eu.apache.org/dist/spark/KEYS
wget http://www-eu.apache.org/dist/spark/spark-2.1.0/spark-2.1.0-bin-hadoop2.7.tgz.asc

gpg --import KEYS
gpg --verify spark-2.1.0-bin-hadoop2.7.tgz.asc spark-2.1.0-bin-hadoop2.7.tgz

install
sudo tar -xvf spark-2.1.0-bin-hadoop2.7.tgz -C /opt
sudo mv /opt/spark-2.1.0-bin-hadoop2.7/ /opt/spark

cp /opt/spark/conf/spark-env.sh.template /opt/spark/conf/spark-env.sh
in the YARN options
export HADOOP_CONF_DIR=/opt/hadoop/etc/hadoop
hdfs dfs -mkdir /user/gavin
hdfs dfs -chown gavin:gavin /user/gavin
add the following to /opt/hadoop/etc/hadoop/yarn-site.xml
    <property>
        <name>yarn.nodemanager.pmem-check-enabled</name>
        <value>false</value>
    </property>
    <property>
        <name>yarn.nodemanager.vmem-check-enabled</name>
        <value>false</value>
    </property>

as user hadoop run pyspark, should set up the /tmp directory on HDFS now users should be use /tmp 
