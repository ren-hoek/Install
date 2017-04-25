cd /tmp
wget https://repo.continuum.io/archive/Anaconda2-4.3.0-Linux-x86_64.sh
sudo bash Anaconda2-4.3.0-Linux-x86_64.sh
install into /opt/anaconda2

sudo cp /etc/bash.bashrc /etc/bash.bashrc.bak
sudo vim /etc/bash.bashrc
add:
     # add Anaconda path" >> ~/.bashrc
     export PATH="/opt/anaconda2/bin:\$PATH"
sudo adduser conda --home /opt/anaconda2
(password conda)
sudo chown -R conda:conda /opt/anaconda2
sudo chmod -R 775 /opt/anaconda2

add users to group:
sudo usermod -a -G conda gavin
logout and in to make change
