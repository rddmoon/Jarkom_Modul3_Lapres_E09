LAPRES JARKOM MODUL 2

**Soal 1**

Melakukan setting UML sesuai dengan topologi berikut
![image](https://user-images.githubusercontent.com/61223768/100406298-13c87a80-3098-11eb-9226-6731d444f218.png)

* buat `topologi.sh` sebagai berikut

<img width="646" alt="topologi" src="https://user-images.githubusercontent.com/61228737/100422378-c8749300-30bc-11eb-917b-6c0a4b775586.png">

* buat `bye.sh` sebagai berikut

<img width="280" alt="bye" src="https://user-images.githubusercontent.com/61228737/100422382-cb6f8380-30bc-11eb-8e97-06660fc30294.png">

* Setting router SURABAYA pada `/etc/sysctl.conf` lalu
* un-comment `net.ipv4.ip_forward=1` 
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

<img width="380" alt="relay" src="https://user-images.githubusercontent.com/61228737/100420643-5c446000-30b9-11eb-89ca-1e82af08f41d.png">

* lakukan `service isc-dhcp-relay restart` untuk menjalankan dhcp-relay

**soal 3**

Setting client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan
192.168.0.110 sampai 192.168.0.200.
* Install `isc-dhcp-server` pada uml TUBAN dengan command `apt-get install isc-dhcp-server`
* lakukan setting file `/etc/default/isc-dhcp-server` seperti berikut

<img width="377" alt="server" src="https://user-images.githubusercontent.com/61228737/100420735-839b2d00-30b9-11eb-96a7-2510e4d04219.png">

* lakukan `service isc-dhcp-server restart` untuk menjalankan dhcp-server
* Edit file `/etc/dhcp/dhcpd.conf` dengan konfigurasi sebagai berikut

<img width="389" alt="server2" src="https://user-images.githubusercontent.com/61228737/100421178-76cb0900-30ba-11eb-9f81-53c54a6169fe.png">

* lakukan test pada client subnet 1 yaitu Gresik dan Sidoarjo

<img width="381" alt="no 3 test gresik" src="https://user-images.githubusercontent.com/61228737/100421380-d9bca000-30ba-11eb-8779-056b65607b0f.png">
<img width="379" alt="no 3 test sidoarjo" src="https://user-images.githubusercontent.com/61228737/100421384-dcb79080-30ba-11eb-83c8-8d415b9720f0.png">

**soal 4**

Setting lient pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
* pada file /etc/dhcp/dhcpd.conf pastikan konfigurasi sebagai berikut

<img width="383" alt="server3" src="https://user-images.githubusercontent.com/61228737/100421234-93674100-30ba-11eb-8da0-eb27ef411493.png">

* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server
* lakukan test pada client di subnet 3 yaitu Madiun dan Banyuwangi

<img width="386" alt="no 4 test banyuwangi" src="https://user-images.githubusercontent.com/61228737/100421559-2c965780-30bb-11eb-9996-b94654fdce01.png">
<img width="383" alt="no 4 test madiun" src="https://user-images.githubusercontent.com/61228737/100421562-2e601b00-30bb-11eb-92f4-5ebb3baf38e8.png">

**soal 5**

Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
* pada file /etc/dhcp/dhcpd.conf pastikan konfigurasi sebagai berikut

<img width="382" alt="server4" src="https://user-images.githubusercontent.com/61228737/100421278-a67a1100-30ba-11eb-8499-6b115908cd8d.png">

* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server

**soal 6**

Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client
pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
* pada file /etc/dhcp/dhcpd.conf pastikan konfigurasi sebagai berikut

<img width="381" alt="server5" src="https://user-images.githubusercontent.com/61228737/100421294-ad088880-30ba-11eb-97c8-939b663ed031.png">

* Jalankan `service isc-dhcp-server restart` untuk menjalankan dhcp-server

**soal 7**

Setting user autentikasi
* lakukan instalasi squid
* lakukan setting pada `htpasswd -c /etc/squid/passwd userta_e09` dengan password: inipassw0rdta_e09 seperti berikut

<img width="378" alt="no 7" src="https://user-images.githubusercontent.com/61228737/100421597-42a41800-30bb-11eb-88a7-6c7afab35cb4.png">

* berikut hasilnya

<img width="960" alt="no 7 test" src="https://user-images.githubusercontent.com/61228737/100421606-46379f00-30bb-11eb-9991-2503316109de.png">

<img width="960" alt="no 7 test2" src="https://user-images.githubusercontent.com/61228737/100421612-4899f900-30bb-11eb-9504-97c67acc71c4.png">


**soal 8**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Rabu pukul 13.00-18.00.
* Lakukan setting pada `nano /etc/squid/acl.conf` dengan konfigurasi sebagai berikut

`acl AVAILABLE_WORKING time TW 13:00-18:00`

<img width="388" alt="no 8" src="https://user-images.githubusercontent.com/61228737/100421689-754e1080-30bb-11eb-84e3-29d7e3da3a04.png">

* lalu pada `/etc/squid/acl.conf` dapat ditambahkan seperti berikut

<img width="379" alt="no 8 kedua" src="https://user-images.githubusercontent.com/61228737/100421696-767f3d80-30bb-11eb-8b3e-aeb3b944e7a5.png">


**soal 9**

Setting agar Proxy server hanya dapat diakses pada hari Selasa-Kamis pukul 21.00-09.00 keesokan harinya.
* tambahkan code berikut pada `nano /etc/squid/acl.conf` 
```
acl AVAILABLE_WORKING2 time TWH 21:00-23:59
acl AVAILABLE_WORKING3 time WHF 00:00-09:00
```

<img width="384" alt="no 9" src="https://user-images.githubusercontent.com/61228737/100421704-7c751e80-30bb-11eb-9cb5-018f60169b4d.png">

* lalu pada `/etc/squid/acl.conf` dapat ditambahkan seperti berikut

<img width="381" alt="no 9 kedua" src="https://user-images.githubusercontent.com/61228737/100421713-80a13c00-30bb-11eb-8bd8-ebe6d8a4095d.png">

**soal 10**

Setting agar ketika mengakses google.com, maka akan melakukan redirect menuju monta.if.its.ac.id.
* Lakukan setting pada ` /etc/squid/squid.conf` seperti berikut

<img width="383" alt="no 10" src="https://user-images.githubusercontent.com/61228737/100421859-c9f18b80-30bb-11eb-84ed-a11df030bcf0.png">

* berikut hasilnya

<img width="960" alt="no 10 test" src="https://user-images.githubusercontent.com/61228737/100421869-cd851280-30bb-11eb-80a6-8870501dd912.png">

<img width="960" alt="no 10 test 2" src="https://user-images.githubusercontent.com/61228737/100421865-ccec7c00-30bb-11eb-9b51-0f2010fc6ddb.png">

**soal 11**

Setting Proxy server agar dapat mengubah error page default squid menjadi halaman yang disediakan
* menuju ke `cd /usr/share/squid/errors/English`
* lakukan `rm ERR_ACCESS_DENIED`
* download file `wget 10.151.36.202/ERR_ACCESS_DENIED`
* cek hasilnya

<img width="960" alt="no 11 test" src="https://user-images.githubusercontent.com/61228737/100422003-0d4bfa00-30bc-11eb-8afe-bce14beece36.png">

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

<img width="381" alt="no 12 satu" src="https://user-images.githubusercontent.com/61228737/100422036-1937bc00-30bc-11eb-8f88-b5715a6c913e.png">

* buat direktori `mkdir /etc/bind/jarkom`
* kemudian copykan `cp /etc/bind/db.local /etc/bind/jarkom/janganlupa-ta.e09.pw`
* edit file `/etc/bind/jarkom/janganlupa-ta.e09.pw` seperti berikut

<img width="382" alt="no 12" src="https://user-images.githubusercontent.com/61228737/100422033-189f2580-30bc-11eb-9c0c-6f7afaff1d2f.png">

* `service bind9 restart` kemudian proxy sudah bisa dijalankan

<img width="960" alt="no 12 test" src="https://user-images.githubusercontent.com/61228737/100422030-15a43500-30bc-11eb-8a27-758c32d5432c.png">
