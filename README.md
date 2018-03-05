M300 LB1
=========

Für den ersten Teil habe, ich ein Mutli VM erstellt mit einer Web Service und Datenbank. Die beiden Server sind in einen Privaten Netzwerk. Nur der Webserver hat Zugriff nach aussen. (<a href="https://github.com/mc-b/devops/tree/master/vagrant">Hier</a> befinden sich die Code und die Files)
 
Mit dieser Vagrantfile wird ein VM mit Debian Linux erstellt. 

Hier die ersten Zeilen des Vagrantfiles in dem die Grundeinstellung der VM definiert werden können.

IP: 192.168.50.4
Hostname: dhcp
RAM: 1024 MB
VM Box: Debian

In dieser VM wird ein DHCP Service installiert.
```
sudo apt-get -y install isc-dhcp-server
```

Der DHCP-Server wird mit dieser Konfiguration installiert. Die Konfigurationfile befindet sich in /etc/dhcp/dhcpd.conf.

Subnet -->   192.168.50.0/24

Range -->    192.168.50.50 - 90

Gateway -->  192.168.50.1

DNS -->      8.8.8.8 (Google DNS)

Domain -->   labor.local
```
sudo sed -i 's/example.org/labor.local/g' /etc/dhcp/dhcpd.conf
sudo sed -i 's/ns2.labor.local/8.8.8.8/g' /etc/dhcp/dhcpd.conf
sudo sed -i '$asubnet 192.168.50.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf
sudo sed -i '$arange 192.168.50.50 192.168.50.90 {' /etc/dhcp/dhcpd.conf
sudo sed -i '$aoption routers 192.168.50.1;' /etc/dhcp/dhcpd.conf
``` 
Die Tastaturlayout ist Deutsch Schweiz.
```
sudo sed -i 's/LANG=en_US.UTF-8/LANG=de_CH.UTF-8/g' /etc/default/local
```
