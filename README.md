M300 LB1
=========

Info
----

Für den ersten Teil habe, ich ein Mutli VM erstellt mit einer Web Service und Datenbank. Die beiden Server sind in einen Privaten Netzwerk. Nur der Webserver hat Zugriff nach aussen. (<a href="https://github.com/mc-b/devops/tree/master/vagrant">Hier</a> befinden sich die Code und die Files)
 
Mit dieser Vagrantfile wird ein VM mit Debian Linux erstellt. 

Hier die ersten Zeilen des Vagrantfiles in dem die Grundeinstellung der VM definiert werden können.

 * IP: 192.168.50.4
 * Hostname: dhcp
 * RAM: 1024 MB
 * VM Box: Debian

In dieser VM wird ein DHCP Service installiert.
```
sudo apt-get -y install isc-dhcp-server
```

Der DHCP-Server wird mit dieser Konfiguration installiert. Die Konfigurationfile befindet sich in /etc/dhcp/dhcpd.conf.

* Subnet: 192.168.50.0/24

* Range: 192.168.50.50 - 90

* Gateway: 192.168.50.1

* DNS: 8.8.8.8 (Google DNS)

* Domain: labor.local
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
Am Schluss wird noch eine lokale Firewall installiert und konfiguriert. Damit wir per SSH zugreifen können wird der Port 22 geöffnet.

```
sudo apt-get -y install ufw gufw 
sudo ufw allow from 10.0.2.2 to any port 22
sudo ufw --force enable
```

HOW TO
------

Im devops Ordner einen neuen Ordner (dhcp-server) erstellen.
Vagrantfile im neuen Ordner abspeichern.

SHELL öffnen und ins Verzeichnis des Vagrantfiles wechseln und diesen Code eingeben.
```
vagrant up
```

Testen
------

Um den DHCP Server zum Testen gibt es zwei Methoden.

**1. Methode**
Im VM das Tool <a href="http://github.com/saravana815/dhtest" dhcptest</a> installieren.
Nach der Installation im Shell dhcptest ausführen.
Wenn man es mit der Option -v ausführt sieht man auch den DHCP-Datenverkehr.

**2.Methode**
Über Vagrant eine neue VM erstellen und starten. Nachdem Starten überprüfen, ob man eine IP bekommen hat.

 SSH Keys
 --------
 
 Ich habe lokal ein SSH Key im Verzeichnis .ssh erstellt mit dem Befehl:
 ```
 ssh-keygen
 ```
Dies ist mein RSA Public:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDJEYgSau7/eVl4008ESXegQ3xCpxL6vc98v/INL60aOhGgKpx4NNotbojQ8ltZwsPHI5U7OS7t4+2uJKXJdqKt+oHkTbJlCJktZpay1CjknGU9+IpLz6LbQeE992RmYwSRwIP6Wx84+A8EdpvYKgtsgCuBklnhtbzWaZjHKZIM6LtL0OqdaclYx85LQsEbuMPctTXoilc8pauy3I9syudSKeO+baeRTSXi1uCVfXcHPdueqOYV/pxqi8Da/GSj6+0vwDyLnGKqZG1BCPUb2n+wb1xYVOIDIZstfWOjweZJgUdtQ2eQa3ah+Q7ftPyKz8cw6YKb5uvZGNzfZ4041Trx Apay@Apaysarans-MBP.tbz.local
```
Reverse Proxy
-------------



 - 
 Apaysaran Muralitharan
