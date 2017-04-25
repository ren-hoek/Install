Install virtualbox
su -
cp /etc/apt/sources.list /etc/apt/sources.list.bak
echo "deb http://download.virtualbox.org/virtualbox/debian xenial contrib" >> /etc/apt/sources.list

wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

apt-get update
apt-get install virtualbox-5.1
exit

Set up guest additions once an ISO has been installed on the virtual machine
cd /media/<username>/VBOXADDITIONS_5.1.14_112924/
sudo sh ./VBoxLinuxAdditions.run

