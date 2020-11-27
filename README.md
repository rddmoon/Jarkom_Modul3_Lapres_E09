LAPRES JARKOM MODUL 2
**Soal 1**

Melakukan setting UML sesuai dengan topologi berikut
![image](https://user-images.githubusercontent.com/61223768/100406298-13c87a80-3098-11eb-9226-6731d444f218.png)

* Setting router SURABAYA pada `/etc/sysctl.conf lalu`
* un-comment `net.ipv4.ip_forward` 
* Aktifkan dengan command `sysctl -p`
* Buat `iptables.sh` pada uml surabaya dengan konfigurasi

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/16

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.1.0/16
```
* Jalankan iptables.sh
* setting source list pada `nano /etc/apt/sources.list` dengan konfigurasi `deb http://boyo.its.ac.id/debian stretch main contrib non-free`
* Setting interface di tiap uml dengan `nano /etc/network/interfaces` seperti berikut

* uml SURABAYA

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.70.42
netmask 255.255.255.252
gateway 10.151.70.41

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 192.168.1.1
netmask 255.255.255.0

auto eth3
iface eth3 inet static
address 10.151.71.81
netmask 255.255.255.248
```

* uml malang

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.82
netmask 255.255.255.248
gateway 10.151.71.81
```

* uml mojokerto

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.83
netmask 255.255.255.248
gateway 10.151.71.81
```

* uml tuban

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.84
netmask 255.255.255.248
gateway 10.151.71.81
```

* uml gresik

```
auto lo

iface lo inet loopback

auto eth0

iface eth0 inet dhcp 
```

* uml sidoarjo

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

* uml madiun

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

* uml banyuwangi

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

* lakukan `service networking restart` pada masing masing uml


**soal 2**

melakukan setting router surabaya sebagai DHCP relay
* Install `isc-dhcp-relay pada` uml SURABAYA dengan command `apt-get install isc-dhcp-relay`
* lakukan setting pada file `/etc/default/isc-dhcp-relay` seperti berikut
* lakukan `service isc-dhcp-relay restart` untuk menjalankan dhcp-relay

**soal 3**

Setting client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan
192.168.0.110 sampai 192.168.0.200.
* Install `isc-dhcp-server` pada uml TUBAN dengan command `apt-get install isc-dhcp-server`
* lakukan setting file `/etc/default/isc-dhcp-server` seperti berikut
* lakukan `service isc-dhcp-relay restart` untuk menjalankan dhcp-server
* Edit file /etc/dhcp/dhcpd.conf dengan konfigurasi sebagai berikut

**soal 4**

Setting lient pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
* pada file /etc/dhcp/dhcpd.conf tambahkan konfigurasi sebagai berikut
* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server

**soal 5**

Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
* pada file /etc/dhcp/dhcpd.conf tambahkan konfigurasi sebagai berikut
* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server

**soal 6**

Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client
pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
* pada file /etc/dhcp/dhcpd.conf tambahkan konfigurasi sebagai berikut
* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server

**soal 7**

Setting user autentikasi
* lakukan instalasi squid
* lakukan setting pada `htpasswd -c /etc/squid/passwd userta_e09` dengan password: inipassw0rdta_e09


**soal 8**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Rabu pukul 13.00-18.00.
* Lakukan setting pada `nano /etc/squid/acl.conf` dengan konfigurasi sebagai berikut
`acl AVAILABLE_WORKING time TW 13:00-18:00`

**soal 9**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Kamis pukul 21.00-09.00 keesokan harinya.
* tambahkan code berikut pada `nano /etc/squid/acl.conf` 
```
acl AVAILABLE_WORKING2 time TWH 21:00-23:59
acl AVAILABLE_WORKING3 time WHF 00:00-09:00
```

**soal 10**

Setting agar ketika mengakses google.com, maka akan melakukan redirect menuju monta.if.its.ac.id.
* Lakukan setting pada ` /etc/squid/squid.conf` seperti berikut

**soal 11**

Setting Proxy server agar dapat mengubah error page default squid menjadi halaman yang disediakan
* menuju ke `cd /usr/share/squid/errors/English`
* lakukan `rm ERR_ACCESS_DENIED`
* download file `wget 10.151.36.202/ERR_ACCESS_DENIED`
* lakukan setting `/etc/squid/squid.conf` dengan menambhakna code

`error_directory /usr/share/squid/errors/English/`

**soal 12**

Setting DNS server agar dapat mengakses Proxy server melalui domain janganlupa-ta.t03.pw dengan port 8080.
* pada uml malang lakukan `apt-get update` dan instalasi bind 9 dengan `apt-get install bind9 -y`
* buka file `/etc/bind/named.conf.local` kemudian setting
```
zone "janganlupa-ta.e09.pw" {
	type master;
	file "/etc/bind/jarkom/janganlupa-ta.e09.pw";
};
```
* `service bind9 restart`

