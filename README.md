# CentOS 7 LAMP Kurulumu ve Yapılandırılması
Bu çalışma ile sıfırdan kurulumu yapılan CentOS 7 işletim sistemine LAMP (**Linux-Apache-MySQL-PHP**) kurulumunu ve kurulum sonrası ilk yapılandırılmasını gerçekleştirileceğiz.
### 1. Sistemimizi Güncelleyelim ve Yeniden Başlatalım
    sudo yum update -y && reboot
### 2. Yapılandırma Sürecinde İşimize Yarayacak Yardımcı Paketleri Yükleyelim
    sudo yum nano -y

    export EDITOR=/bin/nano
### 3. Apache Kurulumu ve Çalıştırılması
    sudo yum install httpd mod_ssl -y

    systemctl start httpd && systemctl enable httpd
### 4. MySQL (MariaDB) Kurulumu ve Çalıştırılması
    sudo yum install mariadb mariadb-server -y

    systemctl start mariadb && systemctl enable mariadb

### 4. PHP (7.4) Kurulumu

### 5. Güvenlik Duvarını Ayarlayalım
    firewall-cmd --permanent --zone=public --add-service=http

    firewall-cmd --permanent --zone=public --add-service=https

    firewall-cmd --reload