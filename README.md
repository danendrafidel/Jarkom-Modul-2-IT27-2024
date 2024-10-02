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

## SOAL 6

Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).

## SOAL 7

Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.

## SOAL 8

Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.

## SOAL 9

Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.

## SOAL 10

Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.

## SOAL 11

Setelah pertempuran mereda, warga IT dapat kembali mengakses jaringan luar dan menikmati meme brainrot terbaru, tetapi hanya warga Majapahit saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit.

## SOAL 12

Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache.
