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

<h2>Модуль 2: Организация сетевого администрирования</h2>

<p>Таблица 2. DNS-записи зон</p>

![Image alt](https://github.com/NewErr0r/DEMO2023/blob/main/images/DNS_table.png?raw=true)

<h2><strong>1. Администрирование локальных вычислительных сетей и принятие мер по устранению возможных сбоев</strong></h2>

<h2>Сетевая связанность</h2>
<p><strong>1.1.</strong> Сети, подключенные к <strong>ISP</strong>, считаются внешними:</p>
<p>- Запрещено прямое попадание трафика из внутренних сетей во внешние и наоборот;</p>
<p><strong>1.2.</strong> Обеспечьте настройку служб SSH региона Left:</p>
<p>a. Подключения со стороны внешних сетей по протоколу к платформе управления трафиком <strong>RTR-L</strong> на порт 2244 должны быть перенаправлены на ВМ <strong>Web-L</strong>;</p>
<p>b. Подключения со стороны внешних сетей по протоколу к платформе управления трафиком <strong>RTR-L</strong> на порт 2222 должны быть перенаправлены на ВМ <strong>WEB-R.</strong></p>

<h3><strong>1.1.</strong> Сети, подключенные к <strong>ISP</strong>, считаются внешними:</h3>
<p>Маскарадинг был включён ранее</p>

<h3><strong>1.2.</strong> Обеспечьте настройку служб SSH региона Left:</h3>
<h4>RTR-L</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=2244:proto=tcp:toport=22:toaddr=192.168.200.100
firewall-cmd --permanent --zone=dmz --add-forward-port=port=2222:proto=tcp:toport=22:toaddr=172.16.100.100
firewall-cmd --reload
</pre>
<h4>WEB-L</h4>
<pre>
vim /etc/ssh/sshd_config
...
PermitRootLogin yes
...
</pre>
<pre>systemctl restart sshd</pre>
<h4>WEB-R</h4>
<pre>
vim /etc/ssh/sshd_config
...
PermitRootLogin yes
...
</pre>
<pre>systemctl restart sshd</pre>

<h2><strong>2. Администрирование сетевых ресурсов в информационных системах</strong></h2>

<h2>Инфраструктурные службы.</h2>
<p><strong>2.1.</strong> Выполните настройку первого уровня DNS-системы стенда:</p>
<p>a. Используется ВМ <strong>ISP;</strong></p>
<p>b. Обслуживается зона demo.wsr.</p>
<p>- Наполнение зоны должно быть реализовано в соответствии с Таблицей 2;</p>
<p>c. Сервер делегирует зону int.demo.wsr на <strong>SRV;</strong></p>
<p>- Поскольку <strong>SRV</strong> находится во внутренней сети западного региона, делегирование происходит на внешний адрес маршрутизатора данного региона.</p>
<p>- Маршрутизатор региона должен транслировать соответствующие порты DNS-службы в порты сервера <strong>SRV.</strong></p>
<p>d. Внешний клиент <strong>CLI</strong> должен использовать DNS-службу, развернутую на <strong>ISP</strong>, по умолчанию;</p>
<p><strong>2.2.</strong> Выполните настройку второго уровня DNS-системы стенда;</p>
<p>a. Используется ВМ <strong>SRV;</strong></p>
<p>b. Обслуживается зона int.demo.wsr;</p>
<p>- Наполнение зоны должно быть реализовано в соответствии с Таблицей 2;</p>
<p>c. Обслуживаются обратные зоны для внутренних адресов регионов</p>
<p>- Имена для разрешения обратных записей следует брать из Таблицы 2;</p>
<p>d. Сервер принимает рекурсивные запросы, исходящие от адресов внутренних регионов;</p>
<p>- Обслуживание клиентов(внешних и внутренних), обращающихся к к зоне int.demo.wsr, должно производится без каких либо ограничений по адресу источника;</p>
<p>e. Внутренние хосты регионов (равно как и платформы управления трафиком) должны использовать данную DNS-службу для разрешения всех запросов имен;</p>
<p><strong>2.3.</strong> Выполните настройку первого уровня системы синхронизации времени:</p>
<p>a. Используется сервер <strong>ISP.</strong></p>
<p>b. Сервер считает собственный источник времени верным, stratum=3;</p>
<p>c. Сервер допускает подключение только через внешний адрес соответствующей платформы управления трафиком;</p>
<p>- Подразумевается обращение <strong>SRV</strong> для синхронизации времени;</p>
<p>d. Клиент <strong>CLI</strong> должен использовать службу времени <strong>ISP;</strong></p>
<p>e. Выполните конфигурацию службы второго уровня времени на <strong>SRV.</strong></p>
<p>a. Сервер синхронизирует время с хостом <strong>ISP;</strong></p>
<p>- Синхронизация с другими источникам запрещена;</p>
<p>b. Сервер должен допускать обращения внутренних хостов регионов, в том числе и платформ управления трафиком, для синхронизации времени;</p>
<p>c. Все внутренние хосты(в том числе и платформы управления трафиком) должны синхронизировать свое время с <strong>SRV;</strong></p>
<p><strong>2.5.</strong> Реализуйте файловый SMB-сервер на базе <strong>SRV</strong></p>
<p>a. Сервер должен предоставлять доступ для обмена файлами серверам <strong>WEB-L</strong> и <strong>WEB-R</strong>;</p>
<p>b. Сервер, в зависимости от ОС, использует следующие каталоги для хранения файлов:</p>
<p>− /mnt/storage для система на базе Linux;</p>
<p>− Диск R:\ для систем на базе Windows;</p>
<p>c. Хранение файлов осуществляется на диске (смонтированном по указанным выше адресам), реализованном по технологии RAID типа “Зеркало”;</p>
<p><strong>2.6.</strong> Сервера <strong>WEB-L</strong> и <strong>WEB-R</strong> должны использовать службу, настроенную на <strong>SRV</strong>, для обмена файлами между собой:</p>
<p>a. Служба файлового обмена должна позволять монтирование в виде стандартного каталога Linux;</p>
<p>- Разделяемый каталог должен быть смонтирован по адресу /opt/share;</p>
<p>b. Каталог должен позволять удалять и создавать файлы в нем для всех пользователей;</p>
<p><strong>2.7.</strong> Выполните настройку центра сертификации на базе <strong>SRV:</strong></p>
<p>b. В случае применения решения на базе Linux используется центр сертификации типа OpenSSL и располагается по адресу /var/ca;</p>
<p>c. Выдаваемые сертификаты должны иметь срок жизни не менее 300 дней;</p>
<p>d. Параметры выдаваемых сертификатов:</p>
<p>- Страна RU;</p>
<p>- Организация DEMO.WSR;</p>
<p>- Прочие поля (за исключением CN) должны быть пусты;</p>

<h3><strong>2.1.</strong> Выполните настройку первого уровня DNS-системы стенда:</h3>
<h4>ISP</h4>
<pre>
mkdir /opt/dns
cp /etc/bind/db.local /opt/dns/demo.db
chown -R bind:bind /opt/dns
</pre>
<pre>
vim /etc/bind/named.conf.options
options {
            directory "/var/cache/bind";
            dnssec-validation no;
            allow-query { any; };
            listen-on-v6 { any; };
        };
</pre>
<pre>
vim /etc/bind/named.conf.default-zones
zone "demo.wsr" {
            type master;
            allow-transfer { any; };
            file "/opt/dns/demo.db";
        };
</pre>
<pre>vim /opt/dns/demo.db</pre>

![Image alt]()

<pre>systemctl restatr bind9</pre>
<h4>RTR-L</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=53:proto={tcp,udp}:toport=53:toaddr=192.168.200.200
firewall-cmd --reload
</pre>
