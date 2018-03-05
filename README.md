M300 LB1
=========

Für den ersten Teil habe, ich ein Mutli VM erstellt mit einer Web Service und Datenbank. Die beiden Server sind in einen Privaten Netzwerk. Nur der Webserver hat Zugriff nach aussen. (<a href="https://github.com/mc-b/devops/tree/master/vagrant">Hier</a> befinden sich die Code und die Files)

Mit dieser Vagrantfile wird ein VM mit Debian Linux erstellt. 
In dieser wird ein DHCP Service installiert.

Der DHCP-Server wird mit dieser Konfiguration installiert.

Subnet -->   192.168.50.0/24

Range -->    192.168.50.50 - 90

Gateway -->  192.168.50.1

DNS -->      8.8.8.8 (Google DNS)

Domain -->   labor.local

Die Tastaturlayout ist Deutsch Schweiz.

