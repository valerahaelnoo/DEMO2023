<h1>DEMO2023</h1>

<h1 align='center'>Образец задания</h1>

<h2>Модуль 1: Выполнение работ по проектированию сетевой инфраструктуры</h2>
<h2>Задание модуля 1:</h2>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/topology.png?raw=true)

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
