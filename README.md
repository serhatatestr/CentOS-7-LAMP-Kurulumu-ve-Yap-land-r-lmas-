# CentOS 7 LAMP Kurulumu ve Yapılandırılması
Bu çalışma ile sıfırdan kurulumu yapılan CentOS 7 işletim sistemine LAMP (**Linux-Apache-MySQL-PHP**) kurulumunu ve kurulum sonrası ilk yapılandırılmasını gerçekleştirileceğiz.
### 1. Sistemimizi Güncelleyelim ve Yeniden Başlatalım

    sudo yum update -y && reboot

### 2. Yapılandırma Sürecinde İşimize Yarayacak Yardımcı Paketleri Yükleyelim
**nano isimli editörü yükleyelim**

    sudo yum nano -y

**nano isimli editörü varsayılan olarak tanımlayalım**

    export EDITOR=/bin/nano

### 3. Apache Kurulumu ve Çalıştırılması
**httpd 'yi ve mod_ssl 'i yükleyelim**

    sudo yum install httpd mod_ssl -y

**http 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım**

    systemctl start httpd && systemctl enable httpd

### 4. MySQL (MariaDB) Kurulumu ve Çalıştırılması
**mariadb 'yi yükleyelim**

    sudo yum install mariadb mariadb-server -y

**mariadb 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım**

    systemctl start mariadb && systemctl enable mariadb

### 4. PHP (7.4) Kurulumu

### 5. Güvenlik Duvarını Ayarlayalım
**firewalld 'yi yükleyelim**

    sudo yum install firewalld -y

**firewalld 'yi çalıştırıp her yeniden başlamada otomatik olarak çalıştırılmasını sağlayalım**

    systemctl start firewalld && systemctl enable firewalld

**firewalld ile http servisini ve 80 portunu ulaşılabilir yapalım**

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --add-port=80

**firewalld ile https servisini ve 443 portunu ulaşılabilir yapalım**

    firewall-cmd --permanent --zone=public --add-service=https
    firewall-cmd --permanent --zone=public --add-port=443

**firewalld ile mariadb servisini ve 3306 portunu ulaşılabilir yapalım(isteğe bağlı)**

    firewall-cmd --permanent --zone=public --add-service=mariadb
    firewall-cmd --permanent --zone=public --add-port=3306

**firewalld kurallarını yeniden yükleyelim**

    firewall-cmd --reload
