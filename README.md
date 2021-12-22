# CentOS 7 LAMP Kurulumu ve Yapılandırılması
Bu çalışma ile sıfırdan kurulumu yapılan CentOS 7 işletim sistemine LAMP (**Linux-Apache-MySQL-PHP**) kurulumunu ve kurulum sonrası ilk yapılandırılmasını gerçekleştirileceğiz.
### 1. Sistemimizi Güncelleyelim ve Yeniden Başlatalım

    sudo yum update -y && reboot

### 2. Yapılandırma Sürecinde İşimize Yarayacak Yardımcı Paketleri Yükleyelim
nano isimli editörü yükleyelim

    sudo yum install nano -y

nano isimli editörü varsayılan olarak tanımlayalım

    export EDITOR=/bin/nano

### 3. Apache Kurulumu ve Çalıştırılması
httpd 'yi ve mod_ssl 'i yükleyelim

    sudo yum install httpd mod_ssl -y

http 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım

    systemctl start httpd && systemctl enable httpd

### 4. MySQL (MariaDB) Kurulumu ve Çalıştırılması
mariadb 'yi yükleyelim

    sudo yum install mariadb mariadb-server -y

mariadb 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım

    systemctl start mariadb && systemctl enable mariadb

mariadb 'nin ilk ayarlarını gerçekleştirelim.

    mysql_secure_installation

### 5. PHP (7.x) Kurulumu
PHP (7.x) için gerekli yardımcı kütüphaneleri yükleyelim

    sudo yum install epel-release -y
    sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
    sudo yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm -y 

kütüphane içerisinde PHP (7.x) versiyonunu belirlememizi sağlayan paketi yükleyelim

    sudo yum install yum-utils -y 

kütüphane içerisinde PHP (7.x) versiyonunu belirleyelim

    sudo yum-config-manager --enable remi-php70
    sudo yum-config-manager --enable remi-php71
    sudo yum-config-manager --enable remi-php72
    sudo yum-config-manager --enable remi-php73
    sudo yum-config-manager --enable remi-php74

PHP (7.x) için gerekli paketleri/modülleri yükleyelim

    sudo yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql -y

http 'yi yeniden başlatalım

    systemctl restart http

### 6. Güvenlik Duvarını Ayarlayalım
firewalld 'yi yükleyelim

    sudo yum install firewalld -y

firewalld 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım

    systemctl start firewalld && systemctl enable firewalld

firewalld ile http servisini ve 80 portunu ulaşılabilir yapalım

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --add-port=80

firewalld ile https servisini ve 443 portunu ulaşılabilir yapalım

    firewall-cmd --permanent --zone=public --add-service=https
    firewall-cmd --permanent --zone=public --add-port=443

firewalld ile mariadb servisini ve 3306 portunu ulaşılabilir yapalım(isteğe bağlı)

    firewall-cmd --permanent --zone=public --add-service=mariadb
    firewall-cmd --permanent --zone=public --add-port=3306

firewalld kurallarını yeniden yükleyelim

    firewall-cmd --reload

### Destek ve Sorular 
Bir sorun yaşamanız durumunda şahsıma ait [e-Posta adresinden](mailto:ates.serhat@bilgetopluluk.com?subject=CentOS%207%20LAMP%20Kurulumu%20ve%20Yapılandırılması%20Hak.) ulaşabilirsiniz. 
