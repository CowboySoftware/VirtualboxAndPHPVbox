# Virtualbox + phpVirtualbox
# Virtualbox + PHPVirtualbox

วิธีการติดตั้ง  Virtualbox (Linux)

1. เข้าไป แก้ไข Sourcelist

sudo vi /etc/apt/sources.list

2.เพิ่ม ตำแหน่งของ Repository ของ  Virtualbox

deb http://download.virtualbox.org/virtualbox/debian xxxxx contrib

*** xxxxx คือ  รุ่นที่พัฒนา เช่น Raring ,Saucy, Trusty,Utopic,Vivid

3.เข้าไปดึง Public key สำหรับ Virtualbox จาก Sourcelist

wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

4. ทำการติตตั้ง Virtualbox จาก

sudo apt-get update
sudo apt-get install linux-headers-$(uname -r) build-essential dkms virtualbox-x.x

*** virtualbox-x.x คือ  version แต่ละ virtualbox

5. Download Extension Pack ลงในเครื่อง 

wget http://download.virtualbox.org/virtualbox/4.1.18/Oracle_VM_VirtualBox_Extension_Pack-4.1.18-78361.vbox-extpack

6. ทำการติตตั้ง Extension Pack

sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-X.X.XXXX.vbox-extpack

7. สร้าง User สำหรับ Run Virtualbox (root mode)
sudo useradd -m vbox -G vboxusers 

8. ตั้งรหัสให้กับ vbox 

passwd vbox

9.เข้าไปเพิ่ม  User ที่เข้าไปใช้ งาน VBoxWeb initscrip ของ  Virtualbox
VBOXWEB_USER=vbox

10. เข้าไปสร้าง System Startup โดยใช้
update-rc.d vboxweb-service defaults
service vboxweb-service start 

11. ติงตั้ง Application Server โดยใช้
sudo apt-get install apache2-mpm-prefork apache2-utils apache2.2-bin  apache2 apache2-doc apache2-suexec libapache2-mod-php5 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libapr1 php5-common php5-mysql  php-pear wget

12 เข้าไป Restart Appache2 Service
sudo service apache2 restart

13. เข้าไปใน Folder ทั้เก็บ website ของ Appache2 
cd /var/www/html

14 ทำการ Download phpvirtualbox โดยใช้

wget http://downloads.sourceforge.net/project/phpvirtualbox/phpvirtualbox-x.x-x.zip

15.หลังจากนั้น ก็ทำการแตกไฟล์  แล้วตั้งชื่อใหม่ 
sudo unzip phpvirtualbox-x.x-x.zip
mv phpvirtualbox-x.x-x phpvirtualbox 

16. เข้าไปใน ไฟลืที่เราแตกไฟล์ไว้ 
cd /var/www/html/phpvirtualbox/

17 เข้าไป copy ไฟล์ชื่อ config.php-example แล้วตั้งชื่อว่า  config.php
cp config.php-example config.php

18. เข้าไปแก้ไข config.php
sudo vi config.php
แล้วไปแก้ไข ตามนี้

/* Username / Password for system user that runs VirtualBox */
var $username = 'vbox';
var $password = 'รหัสที่เราตั้งไว้';

หลังจากนันทำการ Restart Appache2 แล้วเข้าไปที่

 http://IP ของ ตัวเอง /phpvirtualbox/

ในกรณีที่ login ไม่ได้  ให้ เข้าไปพิมพ์คำสั่งนี้

VBoxManage setproperty websrvauthlibrary null

