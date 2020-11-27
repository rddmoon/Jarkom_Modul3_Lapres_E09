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

``auto lo
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

**soal 3**

Setting client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan
192.168.0.110 sampai 192.168.0.200.

**soal 4**

Setting lient pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.

**soal 5**

Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP

**soal 6**

Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client
pada subnet 3 mendapatkan peminjaman IP selama 10 menit.

**soal 7**

Setting user autentikasi

**soal 8**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Rabu pukul 13.00-18.00.

**soal 9**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Kamis pukul 21.00-09.00 keesokan harinya.

**soal 10**

Setting agar ketika mengakses google.com, maka akan melakukan redirect menuju monta.if.its.ac.id.

**soal 11**

Setting Proxy server agar dapat mengubah error page default squid menjadi halaman yang disediakan

**soal 12**

Setting DNS server agar dapat mengakses Proxy server melalui domain janganlupa-ta.t03.pw dengan port 8080.
