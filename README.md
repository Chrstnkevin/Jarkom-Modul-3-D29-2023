# Jarkom-Modul-3-D29-2023
| Nama           | NRP            |
| ---------------| ---------------|
| Christian Kevin Emor      | 5025211153      |
| Ferza Noveri     | 5025211097      |

**Untuk memulai petualangan ini kita akan membuat topologi sebagai berikut:**

![image](https://github.com/Chrstnkevin/Jarkom-Modul-3-D29-2023/assets/97864068/799b3123-e99d-405e-b71a-aad791b7d128)


#### dengan ketentuan sebagai berikut ####
| Node           | Kategori           | Image Docker                      | Konfigurasi IP | Alamat IP | Switch |
| -------------- | ------------------ | ---------------------------------- | -------------- | --------- | --------- |
| Aura           | Router (DHCP Relay) | danielcristh0/debian-buster:1.1    | Dynamic        |      |    |
| Himmel         | DHCP Server         | danielcristh0/debian-buster:1.1    | Static         | 10.36.1.1 | Switch 1 ( 10.36.1.0) |
| Heiter         | DNS Server          | danielcristh0/debian-buster:1.1    | Static         | 10.36.1.2 | Switch 1 ( 10.36.1.0) |
| Denken         | Database Server     | danielcristh0/debian-buster:1.1    | Static         | 10.36.2.1 | Switch 2 ( 10.36.2.0) |
| Eisen          | Load Balancer       | danielcristh0/debian-buster:1.1    | Static         | 10.36.2.2 | Switch 2 ( 10.36.2.0) |
| Frieren        | Laravel Worker      | danielcristh0/debian-buster:1.1    | Static         | 10.36.4.3 | Switch 4 ( 10.36.4.0) |
| Flamme         | Laravel Worker      | danielcristh0/debian-buster:1.1    | Static         | 10.36.4.2 | Switch 4 ( 10.36.4.0) |
| Fern           | Laravel Worker      | danielcristh0/debian-buster:1.1    | Static         | 10.36.4.1 | Switch 4 ( 10.36.4.0) |
| Lawine         | PHP Worker          | danielcristh0/debian-buster:1.1    | Static         | 10.36.3.3 | Switch 3 ( 10.36.3.0) |
| Linie          | PHP Worker          | danielcristh0/debian-buster:1.1    | Static         | 10.36.3.2 | Switch 3 ( 10.36.3.0) |
| Lugner         | PHP Worker          | danielcristh0/debian-buster:1.1    | Static         | 10.36.3.1 | Switch 3 ( 10.36.3.0) |
| Revolte        | Client              | danielcristh0/debian-buster:1.1    | Dynamic        |    | 
| Richter        | Client              | danielcristh0/debian-buster:1.1    | Dynamic        |       |
| Sein           | Client              | danielcristh0/debian-buster:1.1    | Dynamic        |      |
| Stark          | Client              | danielcristh0/debian-buster:1.1    | Dynamic        |

# Konfigurasi Topologi
## Router (Aura)
````
# DHCP config for eth0
auto eth0
iface eth0 inet dhcp
up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.36.0.0/16

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.36.1.0
	netmask 255.255.255.0

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.36.2.0
	netmask 255.255.255.0

# Static config for eth3
auto eth3
iface eth3 inet static
	address 10.36.3.0
	netmask 255.255.255.0

# Static config for eth4
auto eth4
iface eth4 inet static
	address 10.36.4.0
	netmask 255.255.255.0
````

## Switch 1
### Himmel (DHCP Server)
````
auto eth0
iface eth0 inet static
	address 10.36.1.1
	netmask 255.255.255.0
	gateway 10.36.1.0
````

### Heiter (DNS Server)
````
auto eth0
iface eth0 inet static
	address 10.36.1.2
	netmask 255.255.255.0
	gateway 10.36.1.0
````

## Switch 2
### Denken
````
auto eth0
iface eth0 inet static
	address 10.36.2.1
	netmask 255.255.255.0
	gateway 10.36.2.0
````

### Eisen
````
auto eth0
iface eth0 inet static
	address 10.36.2.2
	netmask 255.255.255.0
	gateway 10.36.2.0
````

## Switch 3
### Lugner
````
auto eth0
iface eth0 inet static
	address 10.36.3.1
	netmask 255.255.255.0
	gateway 10.36.3.0
hwaddress ether de:d1:c4:8a:f0:98
````
### Linie
````
auto eth0
iface eth0 inet static
	address 10.36.3.2
	netmask 255.255.255.0
	gateway 10.36.3.0
hwaddress ether 0e:d4:46:cb:eb:13
````
### Lawine
````
auto eth0
iface eth0 inet static
	address 10.36.3.3
	netmask 255.255.255.0
	gateway 10.36.3.0
hwaddress ether 2e:94:bd:99:9b:b1
````
### Client
````
auto eth0
iface eth0 inet dhcp
````

## Switch 4
### Ferm
````
auto eth0
iface eth0 inet static
	address 10.36.4.1
	netmask 255.255.255.0
	gateway 10.36.4.0
hwaddress ether 16:5f:1f:80:51:60
````
### Flamme
````
auto eth0
iface eth0 inet static
	address 10.36.4.2
	netmask 255.255.255.0
	gateway 10.363.4.0
hwaddress ether 8e:42:e6:14:1c:05
````
### Frieren
````
auto eth0
iface eth0 inet static
	address 10.36.4.3
	netmask 255.255.255.0
	gateway 10.36.4.0
hwaddress ether ea:d2:24:a3:79:46
````
### Client
````
auto eth0
iface eth0 inet dhcp
````

# Bagian 1
Karena masih banyak spell yang harus dikumpulkan, bantulah para petualang untuk memenuhi kriteria berikut.:
### No 0
> Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.

Atur topologi sesuai dengan peta yang telah disediakan. Lakukan instalasi dan pengaturan pada setiap node. Pastikan juga untuk menyiapkan **DNS server** dengan cara berikut:
````
No 1

echo 'zone "riegel.canyon.d29.com" {
        type master;
        file "/etc/bind/jarkom/riegel.canyon.d29.com";
};

zone "granz.channel.d29.com" {
        type master;
        file "/etc/bind/jarkom/granz.channel.d29.com";
};' > /etc/bind/named.conf.local

echo '
options {
        directory "/var/cache/bind";
        forwarders {
                192.168.122.1;
        };
        allow-query{any;};
        auth-nxdomain no;       # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/granz.channel.d29.com
cp /etc/bind/db.local /etc/bind/jarkom/riegel.canyon.d29.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.d29.com. root.riegel.canyon.d29.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.d29.com.
@       IN      A       10.36.4.1	; IP Ferm
www     IN      CNAME   riegel.canyon.d29.com.' > /etc/bind/jarkom/riegel.canyon.d29.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.d29.com. root.granz.channel.d29.com. (
                        2023111402      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.d29.com.
@       IN      A       10.36.3.1       ; IP Lugner
www     IN      CNAME   granz.channel.d29.com.' > /etc/bind/jarkom/granz.channel.d29.com

service bind9 restart
````

### No 1-5
> Semua CLIENT harus menggunakan konfigurasi dari DHCP Server
> - Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 (2)
> - Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 (3)
> - Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut (4)
> - Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit (5)

jalankan konfigurasi pada **DHCP Server** seperti berikut
````
echo ' INTERFACES="eth0"
' > /etc/default/isc-dhcp-server

echo 'default-lease-time 600;
max-lease-time 7200;

authoritative;

#eth1
subnet 10.36.1.0 netmask 255.255.255.0 {
}

#eth2
subnet 10.36.2.0 netmask 255.255.255.0 {
}

#eth3
subnet 10.36.3.0 netmask 255.255.255.0 {
    range 10.36.3.16 10.36.3.32;
    range 10.36.3.64 10.36.3.80;
    option routers 10.36.3.0;
    option broadcast-address 10.36.3.255;
    option domain-name-servers 10.36.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

#eth4
subnet 10.36.4.0 netmask 255.255.255.0 {
    range 10.36.4.12 192.185.4.20;
    range 10.36.4.160 192.185.4.168;
    option routers 10.36.4.0;
    option broadcast-address 10.36.4.255;
    option domain-name-servers 10.36.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
service isc-dhcp-server status
````
## Bagian 2
Berjalannya waktu, petualang diminta untuk melakukan deployment.
### No 6-8
> Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3. (6)
> Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
> - Lawine, 4GB, 2vCPU, dan 80 GB SSD.
> - Linie, 2GB, 2vCPU, dan 50 GB SSD.
> - Lugner 1GB, 1vCPU, dan 25 GB SSD.
> aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second. (7)
> Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
> - Nama Algoritma Load Balancer
> - Report hasil testing pada Apache Benchmark
> - Grafik request per second untuk masing masing algoritma.
> - Analisis (8)
### No 9-12
> Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire. (9)
> Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/ (10)
> Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. (11) hint: (proxy_pass)
> Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. (12) hint: (fixed in dulu clinetnya)


## Bagian 3
Karena para petualang kehabisan uang, mereka kembali bekerja untuk mengatur riegel.canyon.yyy.com.
### No 13-20
> Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern. (13)
> Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer (14)
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
> a. POST /auth/register (15)
> b. POST /auth/login (16)
> c. GET /me (17)
> Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern. (18)
> Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
> - pm.max_children
> - pm.start_servers
> - pm.min_spare_servers
> - pm.max_spare_servers
> sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.(19)
> Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second. (20)

