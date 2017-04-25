
download and install latest zeppelin
wget http://www-eu.apache.org/dist/zeppelin/zeppelin-0.7.0/zeppelin-0.7.0-bin-all.tgz

verify download
wget http://www-eu.apache.org/dist/zeppelin/KEYS
wget http://www-eu.apache.org/dist/zeppelin/zeppelin-0.7.0/zeppelin-0.7.0-bin-all.tgz.asc

gpg --import KEYS
gpg --verify zeppelin-0.7.0-bin-all.tgz.asc zeppelin-0.7.0-bin-all.tgz

install
sudo tar -xvf zeppelin-0.7.0-bin-all.tgz -C /opt
sudo mv /opt/zeppelin-0.7.0-bin-all.tgz/ ~/zeppelin

cp zeppelin/conf/zeppelin-env.sh.template zeppelin/conf/zeppelin-env.sh
vim zeppelin/conf/zeppelin-env.sh
export MASTER=yarn-client  
export SPARK_HOME=/opt/spark
export HADOOP_CONF_DIR=/opt/hadoop/etc/hadoop 

./zeppelin/bin/zeppelin-daemon.sh start
(zeppelin will start on port 8080 if spark in standalone mode causes a port conflict)
