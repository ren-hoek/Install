mkdir ~/Install/Apache/Hadoop
cd  ~/Install/Apache/Hadoop
wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz
wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz.asc
wget http://www-eu.apache.org/dist/hadoop/common/KEYS
gpg --import KEYS
gpg --verify hadoop-2.7.3.tar.gz.asc hadoop-2.7.3.tar.gz

sudo tar -xvf hadoop-2.7.3.tar.gz -C /opt
sudo mv /opt/hadoop-2.7.3 /opt/hadoop
adduser hadoop --home /opt/hadoop
sudo cp ~/.bashrc /opt/hadoop
sudo cp ~/.bash_logout /opt/hadoop
sudo cp ~/.profile /opt/hadoop

copy the following to hadoop's .bashrc (might not to needed)
export HADOOP_PREFIX="/opt/hadoop"
export HADOOP_HOME=$HADOOP_PREFIX
export HADOOP_COMMON_HOME=$HADOOP_PREFIX
export HADOOP_CONF_DIR=$HADOOP_PREFIX/etc/hadoop
export HADOOP_HDFS_HOME=$HADOOP_PREFIX
export HADOOP_MAPRED_HOME=$HADOOP_PREFIX
export HADOOP_YARN_HOME=$HADOOP_PREFIX


(password hadoop)
sudo chown -R hadoop:hadoop /opt/hadoop
su - hadoop

add to /opt/hadoop/etc/hadoop/core-site.xml in the configuration
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>

add to /opt/hadoop/etc/hadoop/hdfs-site.xml in the configuration
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>

set up passwordless ssh
sudo ufw allow 22/tcp

need to install openssh-server
sudo apt-get opensh-server

ssh-keygen -t rsa
cat .ssh/id_rsa.pub >> .ssh/authorized_keys
chmod 700 .ssh/
chmod 640 .ssh/authorized_keys 
add JAVA_HOME to vim etc/hadoop/hadoop-env.sh 
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"

bin/hdfs namenode -format
sbin/start-dfs.sh

bin/hdfs dfs -mkdir /user
bin/hdfs dfs -mkdir /user/hadoop

bin/hdfs dfs -put etc/hadoop input
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'

bin/hdfs dfs -cat output/*
sbin/stop-dfs.sh

Set up yarn
Configure parameters as follows:etc/hadoop/mapred-site.xml in configuration:
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>

etc/hadoop/yarn-site.xml:
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>

sbin/start-yarn.sh

sbin/stop-yarn.sh

add the following to the /etc/bash.bashrc
export PATH=$PATH:$HADOOP_PREFIX/bin:$HADOOP_PREFIX/sbin:$JAVA_HOME/bin
