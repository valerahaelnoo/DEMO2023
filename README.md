<h1>DEMO2023</h1>

<h1 align='center'>Образец задания</h1>

<h2>Модуль 1: Выполнение работ по проектированию сетевой инфраструктуры</h2>
<h2>Задание модуля 1:</h2>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/topology.png?raw=true)

<h2><strong>1. Выполнение проектирования кабельной структуры компьютерной сети.</strong></h2>

<h2>Виртуальные машины и коммутация</h2>
<p>Необходимо выполнить создание и базовую конфигурацию виртуальных машин.</p>
<p><strong>1.1.</strong> На основе предоставленных ВМ или шаблонов ВМ создайте отсутствующие виртуальные машины в соответствии со схемой.</p>
<p>a. Характеристики ВМ установите в соответствии с <strong>Таблицей 1;</strong></p>
<p>b. Коммутацию (если таковая не выполнена) выполните в соответствии со схемой сети</p>
<p><strong>1.2.</strong> Имена хостов в созданных ВМ должны быть установлены в соответствии со схемой.</p>
<p><strong>1.3.</strong> Адресация должна быть выполнена в соответствии с Таблицей 1;</p>
<p><strong>1.4.</strong> Обеспечьте ВМ дополнительными дисками, если таковое необходимо в соответствии с <strong>Таблицей 1;</strong></p>
<br>
<p>Таблица 1 Характеристики ВМ</p>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/Specifications_VM.png?raw=true)

________________________________________________________________________________________________________________________________________________________________
<h3><strong>1.1.</strong> На основе предоставленных ВМ или шаблонов ВМ создайте отсутствующие виртуальные машины в соответствии со схемой.</h3>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/1.1.png?raw=true)

<h3><strong>1.2.</strong> Имена хостов в созданных ВМ должны быть установлены в соответствии со схемой.</h3>
<h4>ISP</h4>
<pre>hostnamectl set-hostname ISP</pre>
<h4>RTR-L</h4>
<pre>hostnamectl set-hostname RTR-L</pre>
<h4>RTR-R</h4>
<pre>hostnamectl set-hostname RTR-R</pre>
<h4>SRV</h4>
<pre>Rename-Computer -NewName SRV<br>Restart-Computer</pre>
<h4>WEB-L</h4>
<pre>hostnamectl set-hostname WEB-L</pre>
<h4>WEB-R</h4>
<pre>hostnamectl set-hostname WEB-R</pre>
<h4>CLI</h4>
<pre>Rename-Computer -NewName CLI<br>Restart-Computer</pre>

<h3><strong>1.3.</strong> Адресация должна быть выполнена в соответствии с Таблицей 1;</h3>
<h4>ISP</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim bind9</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 4.4.4.1
netmask 255.255.255.0<br>
auto enp0s8
iface enp0s8 inet static
address 5.5.5.1
netmask 255.255.255.0<br>
auto enp0s9
iface enp0s9 inet static
address 3.3.3.1
netmask 255.255.255.0
dns-search demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>RTR-L</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 4.4.4.100
netmask 255.255.255.0
gateway 4.4.4.1<br>
auto enp0s8
iface enp0s8 inet static
address 192.168.200.254
netmask 255.255.255.0
dns-search int.demo.wsr
dns-nameservers 192.168.200.200
</pre>
<pre>
systemctl restart networking
</pre>
<h4>RTR-R</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 5.5.5.100
netmask 255.255.255.0
gateway 5.5.5.1<br>
auto enp0s8
iface enp0s8 inet static
address 172.16.100.254
netmask 255.255.255.0
dns-search int.demo.wsr
dns-nameservers 192.168.200.200
</pre>
<pre>
systemctl restart networking
</pre>
<h4>SRV</h4>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/SRV_ipv4.png?raw=true)

<h4>WEB-L</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 192.168.200.100
netmask 255.255.255.0
gateway 192.168.200.254
dns-nameservers 192.168.200.200
dns-search int.demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>WEB-R</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 172.16.100.100
netmask 255.255.255.0
gateway 172.16.100.254
dns-nameservers 192.168.200.200
dns-search int.demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>CLI</h4>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/CLI_ipv4.png?raw=true)

<h3><strong>1.4.</strong> Обеспечьте ВМ дополнительными дисками, если таковое необходимо в соответствии с <strong>Таблицей 1;</strong></h3>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/SRV_disks.png?raw=true)

<h2><strong>2. Осуществление выбора технологии, инструментальных средств и средств вычислительной техники при организации процесса разработки и исследования объектов профессиональной деятельности</strong></h2>

<h2>Сетевая связанность</h2>
<p><strong>2.1.</strong> Настройте статический маршрут по умолчанию на маршрутизаторах <strong>RTR-L</strong> и <strong>RTR-R.</strong></p>
<p><strong>2.2.</strong> Настройте динамическую трансляцию портов (PAT):</p>
<p>- На маршрутизаторе <strong>RTR-L</strong> настройте динамическую трансляцию портов (PAT) для сети 192.168.200.0/24 в соответствующие адреса исходящего интерфейса</p>
<p>- На маршрутизаторе <strong>RTR-R</strong> настройте динамическую трансляцию портов (PAT) для
сети 172.16.100.0/24 в соответствующие адреса исходящего интерфейса.</p>

<h2>Конфигурация виртуальных частных сетей</h2>
<p><strong>2.3.</strong> Между платформами <strong>RTR-L</strong> и <strong>RTR-R</strong> должен быть установлен туннель, позволяющий осуществлять связь между регионами с применением внутренних адресов со следующими параметрами:</p>
<p>a) Используйте в качестве VTI интерфейс Tunnel1</p>
<p>b) Между платформами должен быть установлен туннель, позволяющий осуществлять связь между регионами с применением внутренних адресов</p>

<h2>Настройка маршрутизации</h2>
<p><strong>2.4.</strong> Настройте динамическую маршрутизацию между платформами <strong>RTR-L</strong> и <strong>RTR-R.</strong></p>
<p><strong>2.5.</strong> Трафик, идущий по туннелю между регионами по внутренним адресам, не должен транслироваться.</p>


<h3><strong>2.1.</strong> Настройте статический маршрут по умолчанию на маршрутизаторах <strong>RTR-L</strong> и <strong>RTR-R.</strong></h3>
<p> На всех роутерах маршрут по умолчанию задан в качестве шлюза во время назначения адресации в соответствие с Таблицей 1 и является статическим, но необходимо на всех роутерах включить пересылку пакетов! p.s. заодно выключить apparmor (SELinux но для Debian)<p>
<h4>ISP</h4>
<pre>
systemctl disable --now apparmor
echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
sysctl -p
</pre>
<h4>RTR-L</h4>
<pre>
systemctl disable --now apparmor
echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
sysctl -p
</pre>
<h4>RTR-R</h4>
<pre>
systemctl disable --now apparmor
echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
sysctl -p
</pre>
<h3><strong>2.2.</strong> Настройте динамическую трансляцию портов (PAT):</h3>
<h4>RTR-L</h4>
<pre>
apt install -y firewalld<br>
firewall-cmd --permanent --zone=dmz --add-interface=enp0s3
firewall-cmd --permanent --zone=dmz --add-masquerade
firewall-cmd --permanent --zone=trusted --add-interface=enp0s8
firewall-cmd --reload
</pre>
<h4>RTR-R</h4>
<pre>
apt install -y firewalld<br>
firewall-cmd --permanent --zone=dmz --add-interface=enp0s3
firewall-cmd --permanent --zone=dmz --add-masquerade
firewall-cmd --permanent --zone=trusted --add-interface=enp0s8
firewall-cmd --reload
</pre>
<h3><strong>2.3.</strong> Между платформами <strong>RTR-L</strong> и <strong>RTR-R</strong> должен быть установлен туннель, позволяющий осуществлять связь между регионами с применением внутренних адресов со следующими параметрами:</h3>
<h4>RTR-L</h4>
<pre>vim /etc/network/interfaces</pre>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/RTR-L_GRE.png?raw=true)

<pre>systemctl restart networking </pre>
<h4>RTR-R</h4>
<pre>vim /etc/network/interfaces</pre>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/RTR-R_GRE.png?raw=true)

<pre>systemctl restart networking </pre>

<h3><strong>2.4.</strong> Настройте динамическую маршрутизацию между платформами <strong>RTR-L</strong> и <strong>RTR-R.</strong></h3>
<h4>RTR-L</h4>
<p>подключить debian-11.6.0-amd64-BD-2</P>
<pre>
apt-cdrom add
apt install -y frr
</pre>
<pre>
vim /etc/frr/daemons<br>
...
ospfd=yes
...
</pre>
<pre>
systemctl restart frr
systemctl enable frr
</pre>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/RTR-L_OSPF.png?raw=true)

<h4>RTR-R</h4>
<p>подключить debian-11.6.0-amd64-BD-2</P>
<pre>
apt-cdrom add
apt install -y frr
</pre>
<pre>
vim /etc/frr/daemons<br>
...
ospfd=yes
...
</pre>
<pre>
systemctl restart frr
systemctl enable frr
</pre>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/RTR-R_OSPF.png?raw=true)

<h3><strong>2.5.</strong> Трафик, идущий по туннелю между регионами по внутренним адресам, не должен транслироваться.</h3>
<h4>RTR-L</h4>
<pre>
firewall-cmd --permanent --zone=internal --add-inteface=gre1
firewall-cmd --permanent --zone=internal --add-protocol={gre,ospf}
firewall-cmd --permanent --zone=dmz --add-protocol={gre,ospf}
firewall-cmd --reload
</pre>
<h4>RTR-R</h4>
<pre>
firewall-cmd --permanent --zone=internal --add-inteface=gre1
firewall-cmd --permanent --zone=internal --add-protocol={gre,ospf}
firewall-cmd --permanent --zone=dmz --add-protocol={gre,ospf}
firewall-cmd --reload
</pre>
