# Jarkom-Modul-2-IT27-2024

## IT 27

| No  | Nama Anggota          | NRP        |
| --- | --------------------- | ---------- |
| 1   | Danendra Fidel Khansa | 5027231063 |
| 2   | Farida Qurrotu A'yuna | 5027231015 |

## Topologi Kelompok IT27 Praktikum Modul 2

![Topologi](./img/Topologi.png)

## SOAL 1

Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave.

### Router (Nusantara)

Pada topologi ini router terhubung dengan 2 switch

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
  address 10.77.1.1
  netmask 255.255.255.0

auto eth2
iface eth2 inet static
  address 10.77.2.1
  netmask 255.255.255.0

up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.77.0.0/16
```

### Sriwijaya (DNS Master)

Setup untuk bind9

```
auto eth0
iface  eth0 inet static
  address 10.77.2.5
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Majapahit (DNS Slave)

Setup untuk bind9

```
auto eth0
iface  eth0 inet static
  address 10.77.1.2
  netmask 255.255.255.0
  gateway 10.77.1.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Mulawarman (CLient)

Set untuk nameserver DNS Master dan Slave

```
auto eth0
iface  eth0 inet static
  address 10.77.1.3
  netmask 255.255.255.0
  gateway 10.77.1.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### GrahamBell (Client)

Set untuk nameserver DNS Master dan Slave

```
auto eth0
iface  eth0 inet static
  address 10.77.1.4
  netmask 255.255.255.0
  gateway 10.77.1.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Samaratungga (Client)

Set untuk nameserver DNS Master dan Slave

```
auto eth0
iface  eth0 inet static
  address 10.77.1.5
  netmask 255.255.255.0
  gateway 10.77.1.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Srikandi (Client)

Set untuk nameserver DNS Master dan Slave

```
auto eth0
iface  eth0 inet static
  address 10.77.2.3
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Kotalingga (Web Server)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.4
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Tanjungkulai (Web Server)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.6
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Bedahulu (Web Server)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.7
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Solok (Load Balancer)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.2
  netmask 255.255.255.0
  gateway 10.77.2.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

## SOAL 2

Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.

## SOAL 3

Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

## SOAL 4

Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.

## SOAL 5

Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.

- Tambahkan nameserver prefix ip `10.77.2.5` pada `etc/resolv.conf`

- coba dengan memasukkan pada client

```
ping www.sudarsana.it27.com
ping www.pasopati.it27.com
ping.www.rujapala.it27.com
```

![5](./img/5.png)

## SOAL 6

Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).

- Edit untuk DNS Master `/etc/bind/named.conf.local` nambahin PTR

```
zone "2.77.10.in-addr.arpa" {
    type master;
    file "/etc/bind/it27/2.77.10.in-addr.arpa";
};
```

- Copy `cp /etc/bind/db.local /etc/bind/it27/2.77.10.in-addr.arpa`

- cd ke `/etc/bind/it27` lalu edit `nano 2.77.10.in-addr.arpa` tambhain yang dibawah itu

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it27.com. root.pasopati.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.77.10.in-addr.arpa.   IN      NS      pasopati.it27.com.
4                       IN      PTR     pasopati.it27.com.
```

- Restart `service bind9 restart`

- Coba di client dengan `host -t PTR 10.77.2.4`

![6](./img/6.png)

## SOAL 7

Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.

- Pada DNS Master edit `/etc/bind/named.conf.local` untuk `notify` dan `also-notify`

```

zone "sudarsana.it27.com" {
type master;
notify yes;
also-notify { 10.77.1.2;};
file "/etc/bind/it27/sudarsana.it27.com";
};

zone "pasopati.it27.com" {
type master;
notify yes;
also-notify { 10.77.1.2;};
file "/etc/bind/it27/pasopati.it27.com";
};

zone "rujapala.it27.com" {
type master;
notify yes;
also-notify { 10.77.1.2;};
file "/etc/bind/it27/rujapala.it27.com";
};

zone "2.77.10.in-addr.arpa" {
type master;
notify yes;
also-notify { 10.77.1.2;};
file "/etc/bind/it27/2.77.10.in-addr.arpa";
};

```

- Kemudian pada DNS Slave edit `/etc/bind/named.conf.local` untuk type `slave`

```

zone "sudarsana.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/sudarsana.it27.com";
};

zone "pasopati.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/pasopati.it27.com";
};

zone "rujapala.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/rujapala.it27.com";
};

zone "2.77.10.in-addr.arpa" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/2.77.10.in-addr.arpa";
};
zone "panah.pasopati.it27.com" {
type master;
file "/etc/bind/panah/panah.pasopati.it27.com";
};

```

- Pada DNS Master `service bind9 stop`

![7](<./img/7%20(1).png>)

- Kemudian pada DNS Slave `service bind9 restart`

![7](<./img/7%20(2).png>)

- Ping pada client misal `ping www.sudarsana.it27.com` untuk membuktikan DNS Slave berjalan

![7](<./img/7%20(3).png>)

## SOAL 8

Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.

- Setup pada DNS Master `/etc/bind/it27/sudarsana.it27.com`

```

;
; BIND data file for local loopback interface
;
$TTL 604800
@ IN SOA 10.77.2.2. root.10.77.2.2. (
2 ; Serial
604800 ; Refresh
86400 ; Retry
2419200 ; Expire
604800 ) ; Negative Cache TTL
;
@ IN NS sudarsana.it27.com.
@ IN A 10.77.2.2
@ IN AAAA ::1
www IN CNAME sudarsana.it27.com.
cakra IN A 10.77.2.7

```

- Restart service bind9 di DNS Master `service bind9 restart`

![8](<./img/8%20(2).png>)

- cek subdomain `cakra.sudarsana.it27.com` di client

  ![8](<./img/8%20(3).png>)

## SOAL 9

Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.

- Setup pada DNS Master ` /etc/bind/it27` untuk nambahin subdomain

```

;
; BIND data file for local loopback interface
;
$TTL 604800
@ IN SOA pasopati.it27.com. root.pasopati.it27.com. (
2 ; Serial
604800 ; Refresh
86400 ; Retry
2419200 ; Expire
604800 ) ; Negative Cache TTL
;
@ IN NS pasopati.it27.com.
@ IN A 10.77.2.4
@ IN AAAA ::1
www IN CNAME pasopati.it27.com.
ns1 IN A 10.77.1.2
panah IN NS ns1

```

- Pada DNS Master masih edit `/etc/bind/named.conf.options`

```

options {
    directory "/var/cache/bind";
    //dnssec-validation auto;
    allow-query{any;};

    auth-nxdomain no;    # conform to RFC1035
    listen-on-v6 { any; };
};
```

- Kemudian restart service bind9 `service bind9 restart`

- Kemudian pada DNS Slave setup `nano /etc/bind/named.conf.local` tambahkan untuk subdomain `panah.pasopati.it27.com`

```

zone "sudarsana.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/sudarsana.it27.com";
};

zone "pasopati.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/pasopati.it27.com";
};

zone "rujapala.it27.com" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/rujapala.it27.com";
};
zone "2.77.10.in-addr.arpa" {
type slave;
masters {10.77.2.5;};
file "/var/lib/bind/it27/2.77.10.in-addr.arpa";
};
zone "panah.pasopati.it27.com" {
type master;
file "/etc/bind/panah/panah.pasopati.it27.com";
};

```

- Buat direktori panah `/etc/bind/panah`

- Lalu cp `cp /etc/bind/db.local /etc/bind/panah/panah.pasopati.it27.com`

![9](<./img/9%20(3).png>)

- Edit `named.conf.local` untuk nambahin subdomainnya seperti dibawah pada DNS Slave

```

;
; BIND data file for local loopback interface
;
$TTL 604800
@ IN SOA panah.pasopati.it27.com. root.panah.pasopati.it27.com. (
2 ; Serial
604800 ; Refresh
86400 ; Retry
2419200 ; Expire
604800 ) ; Negative Cache TTL
;
@ IN NS panah.pasopati.it27.com.
@ IN A 10.77.2.4
@ IN AAAA ::1
www IN CNAME panah.pasopati.it27.com

```

- Restart bind9 `service bind9 restart`

- `ping panah.pasopati.it27.com` pada client

![9](<./img/9%20(4).png>)

## SOAL 10

Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.

- Masuk kedalam `cd /etc/bind/panah`
- Tambahkan subdomain lognya

```

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it27.com. root.panah.pasopati.it$
2 ; Serial
604800 ; Refresh
86400 ; Retry
2419200 ; Expire
604800 ) ; Negative Cache TTL
;
@ IN NS panah.pasopati.it27.com.
@ IN A 10.77.2.4
@ IN AAAA ::1
www IN CNAME panah.pasopati.it27.com
log IN A 10.77.2.4
www.log IN CNAME panah.pasopati.it27.com

```

- Restart dengan `service bind9 restart`

- Ping pada client `ping log.panah.pasopati.it27.com`

![10](./img/10.png)

## SOAL 11

Setelah pertempuran mereda, warga IT dapat kembali mengakses jaringan luar dan menikmati meme brainrot terbaru, tetapi hanya warga Majapahit saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit.

- Edit `/etc/bind/named.conf.options`

![11](<./img/11%20(1).png>)

- Restart `service bind9 restart`
- Ping pada client `ping google.com`

![11](<./img/11%20(2).png>)

## SOAL 12

Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache.

## SOAL 13

Karena Sriwijaya dan Majapahit memenangkan pertempuran ini dan memiliki banyak uang dari hasil penjarahan (sebanyak 35 juta, belum dipotong pajak) maka pusat meminta kita memasang load balancer untuk membagikan uangnya pada web nya, dengan Kotalingga, Bedahulu, Tanjungkulai sebagai worker dan Solok sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya.

## SOAL 14

Selama melakukan penjarahan mereka melihat bagaimana web server luar negeri, hal ini membuat mereka iri, dengki, sirik dan ingin flexing sehingga meminta agar web server dan load balancer nya diubah menjadi nginx.

## SOAL 15

Markas pusat meminta laporan hasil benchmark dengan menggunakan apache benchmark dari load balancer dengan 2 web server yang berbeda tersebut dan meminta secara detail dengan ketentuan:

- Nama Algoritma Load Balancer
- Report hasil testing apache benchmark
- Grafik request per second untuk masing masing algoritma.
- Analisis
- Meme terbaik kalian (terserah ( ͡° ͜ʖ ͡°)) 🤓

## SOAL 16

Karena dirasa kurang aman dari brainrot karena masih memakai IP, markas ingin akses ke Solok memakai solok.xxxx.com dengan alias www.solok.xxxx.com (sesuai web server terbaik hasil analisis kalian).

## SOAL 17

Agar aman, buatlah konfigurasi agar solok.xxx.com hanya dapat diakses melalui port sebesar π x 10^4 = (phi nya desimal) dan 2000 + 2000 log 10 (10) +700 - π = ?.

## SOAL 18

Apa bila ada yang mencoba mengakses IP solok akan secara otomatis dialihkan ke www.solok.xxxx.com.

## SOAL 19

Karena probset sudah kehabisan ide masuk ke salah satu worker buatkan akses direktori listing yang mengarah ke resource worker2.

## SOAL 20

Worker tersebut harus dapat di akses dengan sekiantterimakasih.xxxx.com dengan alias www.sekiantterimakasih.xxxx.com.
