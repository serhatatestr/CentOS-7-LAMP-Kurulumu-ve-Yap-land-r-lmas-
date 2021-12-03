# CentOS 7 LAMP Kurulumu ve Yapılandırılması
Bu çalışma ile sıfırdan kurulumu yapılan CentOS 7 işletim sistemine LAMP (**Linux-Apache-MySQL-PHP**) kurulumunu ve kurulum sonrası ilk yapılandırılmasını gerçekleştirileceğiz.
### 1. Sistemimizi Güncelleyelim ve Yeniden Başlatalım
    sudo yum update -y && reboot
### 2. Yapılandırma Sürecinde İşimize Yarayacak Yardımcı Paketleri Yükleyelim
    sudo yum nano -y
    export EDITOR=/bin/nano
### 3. Apache Kurulumu ve Çalıştırılması
    sudo yum httpd mod_ssl -y
    systemctl start httpd && systemctl enable httpd
