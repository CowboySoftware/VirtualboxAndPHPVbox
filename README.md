
# Virtualbox + PHPVirtualbox

##### วิธีการติดตั้ง  Virtualbox (Linux)

* เข้าไป แก้ไข Sourcelist
```sh
$ sudo vi /etc/apt/sources.list
```

* เพิ่ม ตำแหน่งของ Repository ของ  Virtualbox
```sh
deb http://download.virtualbox.org/virtualbox/debian xxxxx contrib
```
`` xxxxx คือ  รุ่นที่พัฒนา เช่น Raring ,Saucy, Trusty, Utopic, Vivid``
* เข้าไปดึง Public key สำหรับ Virtualbox จาก Sourcelist
```sh
$ wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```
* ทำการติตตั้ง Virtualbox จาก
```sh
$ sudo apt-get update
$ sudo apt-get install linux-headers-$(uname -r) build-essential dkms virtualbox-x.x
```
`` virtualbox-x.x คือ  version แต่ละ virtualbox``

* Download Extension Pack ลงในเครื่อง 
```sh
$ wget http://download.virtualbox.org/virtualbox/4.1.18/Oracle_VM_VirtualBox_Extension_Pack-x.x.x.vbox-extpack
```
* ทำการติตตั้ง Extension Pack
```sh
$ sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-X.X.XXXX.vbox-extpack
```
* สร้าง User สำหรับ Run Virtualbox (root mode)
```sh
$ sudo useradd -m vbox -G vboxusers 
```
* ตั้งรหัสให้กับ vbox 
```sh
$ sudo passwd vbox
```
* เข้าไปเพิ่ม  User ที่เข้าไปใช้ งาน VBoxWeb initscrip ของ  Virtualbox
(ในกรณีที่ไม่มีไฟล์นั้น create ไฟล์นั้นๆ ขึ้นมา) โดยใช้คำสั่ง

```sh
sudo vi /etc/defaults/virtualbox
```
``
เพิ่ม VBOXWEB_USER=vbox ในไฟล์นั้นๆ
``
* เข้าไปสร้าง System Startup โดยใช้
```sh
$ update-rc.d vboxweb-service defaults
$ service vboxweb-service start 
```
* ติงตั้ง Application Server โดยใช้
```sh
sudo apt-get install apache2-mpm-prefork apache2-utils apache2.2-bin  apache2 apache2-doc apache2-suexec libapache2-mod-php5 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libapr1 php5-common php5-mysql  php-pear wget
```
* เข้าไป Restart Appache2 Service
```sh
$ sudo service apache2 restart
```
* เข้าไปใน Folder ทั้เก็บ website ของ Appache2 
```
$ cd /var/www/html
```
* ทำการ Download phpvirtualbox โดยใช้
```
$ wget http://downloads.sourceforge.net/project/phpvirtualbox/phpvirtualbox-x.x-x.zip
```
* หลังจากนั้น ก็ทำการแตกไฟล์  แล้วตั้งชื่อใหม่ 
```sh
$ sudo unzip phpvirtualbox-x.x-x.zip
$ mv phpvirtualbox-x.x-x phpvirtualbox 
```
* เข้าไปใน ไฟลืที่เราแตกไฟล์ไว้ 
```sh
$ cd /var/www/html/phpvirtualbox/
```
* เข้าไป copy ไฟล์ชื่อ config.php-example แล้วตั้งชื่อว่า  config.php
```sh
$ cp config.php-example config.php
```
* เข้าไปแก้ไข config.php
```sh
$ sudo vi config.php
```
* แล้วไปแก้ไข ตามนี้
```sh
var $username = 'vbox';
var $password = 'รหัสที่เราตั้งไว้';
```
* หลังจากนันทำการ Restart Appache2 แล้วเข้าไปที่
```sh
http://IP ของ ตัวเอง /phpvirtualbox/
```

* ในกรณีที่ login ไม่ได้  ให้ เข้าไปพิมพ์คำสั่งนี้``
```sh
$ sudo VBoxManage setproperty websrvauthlibrary null
```











