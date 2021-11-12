# Jarkom-Modul-3-A03-2021

## Anggota

| Nama | NRP |
| :----: | :----: |
| Jessica Tasyanita | 05111940000043 |
| Daniel Sugianto | 05111940000075 |
| Ryan Fernaldy | 05111940000152 |

## Soal 1

Diminta membuat topologi seperti di bawah dengan ketentuan EniesLobby sebagai DNS Server, Jipangu sebagai DHCP Server, Water7 sebagai Proxy Server.

![topologi](https://user-images.githubusercontent.com/58259649/141461325-5617caea-2985-448a-b6d2-735982ce4857.png)

1. Buat topologi seperti yang diminta.

![topologi_a03](https://user-images.githubusercontent.com/58259649/141462465-edb1012d-31a3-4dab-9e6e-263353f61511.jpg)

2. Ubah network configuration Foosha menjadi seperti berikut.

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 192.170.1.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 192.170.2.1
    netmask 255.255.255.0

auto eth3
iface eth3 inet static
    address 192.170.3.1
    netmask 255.255.255.0

```

3. Pada `root/.bashrc` Foosha, tambahkan line.
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.170.0.0/16
```
4. Untuk setiap node, jalankan command berikut.
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
5. Untuk setiap node selain Foosha, sementara ubah network configuration menjadi seperti berikut untuk keperluan akses internet dan konfigurasi. Network configuration pada Loguetown, Alabasta, TottoLand, dan Skypie akan diubah.

- Loguetown
```
auto eth0
iface eth0 inet static
    address 192.170.1.2
    netmask 255.255.255.0
    gateway 192.170.1.1

```
- Alabasta
```
auto eth0
iface eth0 inet static
    address 192.170.1.3
    netmask 255.255.255.0
    gateway 192.170.1.1
```
- EniesLobby
```
auto eth0
iface eth0 inet static
    address 192.170.2.2
    netmask 255.255.255.0
    gateway 192.170.2.1
```
- Water7
```
auto eth0
iface eth0 inet static
    address 192.170.2.3
    netmask 255.255.255.0
    gateway 192.170.2.1
```
- Jipangu
```
auto eth0
iface eth0 inet static
    address 192.170.2.4
    netmask 255.255.255.0
    gateway 192.170.2.1
```
- TottoLand
```
auto eth0
iface eth0 inet static
    address 192.170.3.2
    netmask 255.255.255.0
    gateway 192.170.3.1
```
- Skypie
```
auto eth0
iface eth0 inet static
    address 192.170.3.3
    netmask 255.255.255.0
    gateway 192.170.3.1
```

6. Install bind9 pada EniesLobby (DNS server).

```
apt-get install bind9 -y
```

7. Install squid pada Water7 (proxy server).

```
apt-get install squid -y
```

8. Install isc-dhcp-server pada Jipangu (DHCP server).

```
apt-get install isc-dhcp-server -y
```

9. Pada `/etc/default/isc-dhcp-server` di node Jipangu, perbarui line `INTERFACES=""` menjadi `INTERFACES="eth0"`.

10. Ubah network configuration Loguetown, Alabasta, TottoLand, dan Skypie menjadi seperti berikut agar node-node tersebut menggunakan konfigurasi IP dari DHCP Server.

```
auto eth0
iface eth0 inet dhcp
```

### Kendala

- Tidak ada

## Soal 2

Menjadikan Foosha sebagai DHCP Relay.

1. Install isc-dhcp-relay pada Foosha

```
apt-get install isc-dhcp-relay
```

2. Ubah `/etc/default/isc-dhcp-relay` pada node Foosha menjadi seperti berikut. `SERVERS` mengarah pada IP Jipangu dan DHCP relay akan melayani DHCP request pada interface eth1, eth2, dan eth3.

![foosha_dhcp_relay](https://user-images.githubusercontent.com/58259649/141465412-1d5314f3-c196-4e08-babe-fbb4194c5fed.jpg)

3. Restart isc-dhcp-relay.

```
service isc-dhcp-relay restart
```

### Kendala
- Tidak ada

## Soal 3

Client yang melalui Switch1 mendapatkan range IP dari 192.170.1.20 - 192.170.1.99 dan 192.170.1.150 - 192.170.1.169

1. Ubah `/etc/dhcp/dhcpd.conf` pada node Jipangu menjadi seperti berikut, sehingga client pada Switch1 mendapat range IP sesuai yang diminta.

![switch1](https://user-images.githubusercontent.com/58259649/141465838-5ab7f91e-682d-4034-b6f4-e65997edcb87.jpg)

2. Restart dhcp server.

```
service isc-dhcp-server restart
```

3. Restart Loguetown dan Alabasta (client pada Switch1) dan jalankan `ip a` untuk melihat IP masing-masing node.

![3_alabasta](https://user-images.githubusercontent.com/58259649/141466190-d5e9ca68-be9e-43d8-aeee-613419bb252a.jpg)

![3_loguetown](https://user-images.githubusercontent.com/58259649/141466199-cdc0427c-3709-464a-b9b3-cb6a3d63f5d0.jpg)

### Kendala
- Tidak ada

## Soal 4

Client yang melalui Switch3 mendapatkan range IP dari 192.170.3.30 - 192.170.3.50

1. Tambahkan line-line berikut di `/etc/dhcp/dhcpd.conf` pada node Jipangu menjadi, sehingga client pada Switch3 mendapat range IP sesuai yang diminta.

![4_dhcpd conf](https://user-images.githubusercontent.com/58259649/141466355-e294a8b4-3066-4483-8047-0cc2f4e2d1e5.jpg)

2. Restart dhcp server.

```
service isc-dhcp-server restart
```

3. Restart TottoLand dan Skypie (client pada Switch3) dan jalankan `ip a` untuk melihat IP masing-masing node.

![4_skypie](https://user-images.githubusercontent.com/58259649/141466737-82c39ddb-8b3c-442a-95f0-0f1a60e07c6d.jpg)

![4_tottoland](https://user-images.githubusercontent.com/58259649/141466757-bad6c254-891f-496d-b16b-951268860745.jpg)

### Kendala
- Tidak ada

## Soal 5
Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut
- EniesLobby<br>
  Mengatur forwarders ke nameserver dari foosha (192.168.122.1) agar client bisa akses internet, comment baris ``dnssec-validation auto;``, menambah baris ``allow-query{any;};``
  ![image](https://user-images.githubusercontent.com/68326540/141309651-69cac9c0-362d-4ac9-9c43-54655a9240a2.png)

- Jipangu<br>
  Mangarahkan ``option domain-name-servers`` ke IP EniesLobby (192.170.2.2)
  ![image](https://user-images.githubusercontent.com/68326540/141310396-22acdb92-ea21-4598-9b93-0710baa7c9c4.png)
  
 - Loguetown<br>
  ![image](https://user-images.githubusercontent.com/68326540/141310276-80b218d1-63df-43f1-a457-1c9a6c9bbc90.png)


### Kendala
- Tidak ada

## Soal 6
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit. 
- Jipangu<br>
  Mengatur ``default-lease-time`` menjadi 360 detik (6 menit) untuk Switch1 dan 720 detik (12 menit) untuk Switch3. Mengatur ``default-lease-time``menjadi 7200 detik (120 menit) untuk Switch1 dan Switch3.
  ![image](https://user-images.githubusercontent.com/68326540/141312271-b3acde5c-46b4-4fa9-85f7-1c26bb5e6e7f.png)

- Loguetown (Switch1)<br>
  ![image](https://user-images.githubusercontent.com/68326540/141312003-a2d3db49-bcad-4f3e-a997-4ca382fba875.png)
- Tottoland (Switch3)<br>
  ![image](https://user-images.githubusercontent.com/68326540/141428557-7c1332c3-170f-4c64-a862-965236877716.png)


### Kendala
- Tidak ada

## Soal 7
Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69 
- Skypie<br>
  Atur hwaddress pada /etc/network/interfaces<br>
  ![image](https://user-images.githubusercontent.com/68326540/141428955-d13973d8-8c8d-4880-b2bc-df95a86a6ce4.png)

- Jipangu<br>
  Menambahkan baris berikut ke /etc/dhcp/dhcpd.conf dimana hardware ethernet yang digunakan disamakan dengan hwaddress yang telah diatur di Skypie<br>
  ```
  host Skypie {
    hardware ethernet e2:a9:e4:73:f8:9c;
    fixed-address 192.170.3.69;
  }
  ```
  ```
  service isc-dhcp-server restart
  ```
- Skypie<br>
  ![image](https://user-images.githubusercontent.com/68326540/141429354-1d577c76-9fc2-4eee-b751-949229d6d860.png)


### Kendala
Tidak ada

## Soal 8
Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi. Pada Loguetown, proxy harus bisa diakses dengan nama jualbelikapal.yyy.com dengan port yang digunakan adalah 5000
- EniesLobby<br>
  - Tambahkan baris berikut pada /etc/bind/named.conf.local
    ```
    zone "jualbelikapal.A03.com" {
      type master;
      file "/etc/bind/jarkom/jualbelikapal.A03.com";
    };
    ```
  - Buat folder /etc/bind/jarkom
    ```
    mkdir /etc/bind/jarkom
    ```
    
  - Atur BIND data pada /etc/bind/jarkom/jualbelikapal.A03.com dengan mengrahakan domain ke IP  Water7 (192.170.2.3) dimana Proxy Server berada 
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL	604800
    @   	IN  	SOA 	jualbelikapal.A03.com. root.jualbelikapal.A03.com. (
                                2     	; Serial
                          604800     	; Refresh
                            86400     	; Retry
                          2419200     	; Expire
                          604800 )   	; Negative Cache TTL
    ;
    @   	IN  	NS  	jualbelikapal.A03.com.
    @   	IN  	A   	192.170.2.3
    ```
  - Restart Bind9
    ```
    service bind9 restart
    ```
- Water7
  - Backup /etc/squid/squid.conf
    ```
    mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
    ```
  - Buat squid.conf yang baru
    ```
    http_port 5000
    visible_hostname jualbelikapal.A03.com
    ```
  - Restart squid
    ```
    service squid restart
    ```
    
- Mangaktifkan proxy di Loguetown<br>
  ![image](https://user-images.githubusercontent.com/68326540/141430302-124ff218-e154-4f53-ba34-05ac04e852f4.png)
  
  ```
  lynx http://its.ac.id
  ```
  ![image](https://user-images.githubusercontent.com/68326540/141433819-db62bd07-995d-4351-a470-eeeb368a0508.png)<br>
  Berhasil menggunakan proxy dengan nama jualbelikapal.A03.com
  
- Menambah permission agar bisa akses web pada /etc/squid/squid.conf di Water7
  ```
  http_access allow all
  ```
- Mengakses web
  ```
  lynx http://its.ac.id
  ```
  ![image](https://user-images.githubusercontent.com/68326540/141430984-a1d17a0c-3632-48ac-aafc-ba0aec52d3b5.png)

### Kendala
 - Tidak ada


## Soal 9
gar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu luffybelikapalyyy dengan password luffy_yyy dan zorobelikapalyyy dengan password zoro_yyy
- Water7
  - Membuat file untuk menyimpan username dan password
    ```
    touch /etc/squid/passwd
    apt-get install apache2 -y
    ```

    ```
    htpasswd -b -m /etc/squid/passwd luffybelikapalA03 luffy_A03
    htpasswd -b -m /etc/squid/passwd zorobelikapalA03 zoro_A03
    ```
    Parameter -b untuk mengambil password secara langsung dari terminal tanpa perlu meminta (prompt) lagi.
    Parameter -m untuk melakukan enkripsi dengan MD5
  - Tambahkan pengaturan di /etc/squid/squid.conf<br>
    ![image](https://user-images.githubusercontent.com/68326540/141432111-7e588407-00a5-4cec-bb0b-48f8a124ea40.png)

  - Restart squid
    ```
    service squid restart
    ```
- Loguetown<br>
  ![image](https://user-images.githubusercontent.com/68326540/141432187-3b174490-5bcd-4e8b-9d50-92787179cc77.png)
  ![image](https://user-images.githubusercontent.com/68326540/141432209-870e13d0-a21e-45e7-a05a-538f32921d9d.png)
  ![image](https://user-images.githubusercontent.com/68326540/141432232-87976c70-40b7-427a-9946-26cd1be3f6d7.png)
  ![image](https://user-images.githubusercontent.com/68326540/141432252-d465ff4b-ef46-4a45-b2e1-e29df66c3bc3.png)


### Kendala
- Sulit mencari syntax untuk enkripsi password

## Soal 10
Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari Senin-Kamis pukul 07.00-11.00 dan setiap hari Selasa-Jum’at pukul 17.00-03.00 keesokan harinya (sampai Sabtu pukul 03.00)
- Water7
  - Membuat file /etc/squid/acl.conf untuk menyimpan waktu dilakukannya pembatasan akses (waktu dimana user tidak bisa akses)
    Sebagai contoh pada hari senin pembatasan akses dilakukan dari pukul 00.00-06.59 dan 11.01-24.00
    ```
    acl UNAVAILABLE1 time S 00:00-24:00
    acl UNAVAILABLE2 time MT 00:00-06:59
    acl UNAVAILABLE3 time M 11:01-24:00
    acl UNAVAILABLE4 time TWH 11:01-16:59
    acl UNAVAILABLE5 time WHF 03:01-16:59
    acl UNAVAILABLE6 time A 03:01-24:00
    ```
  - Melakukan include /etc/squid/acl.conf untuk mengambil waktu pembatasan akses dan menambahkan ``http_access deny`` untuk setiap waktu yang didefinisikan<br>
    ![image](https://user-images.githubusercontent.com/68326540/141433215-bf58b87c-3818-4d29-800f-ab569a635c83.png)
  - Restart squid
    ```
    service squid restart
    ```
- Loguetown
  - Hari Minggu jam 08:00 membuka http://its.ac.id (tidak bisa)
    ```
    date -s "7 Nov 2021 08:00:00"
    lynx http://its.ac.id
    ```
    ![image](https://user-images.githubusercontent.com/68326540/141433473-3cd41e88-967f-4731-b901-8d7502bf96fc.png)
  
  - Hari Selasa jam 17:00 membuka http://its.ac.id (bisa)
    ```
    date -s "9 Nov 2021 17:00:00"
    lynx http://its.ac.id
    ```
    ![image](https://user-images.githubusercontent.com/68326540/141433625-baa0a272-16da-4c08-8459-7da37a5eb1c0.png)

 

### Kendala
- Tidak ada
## Soal 11

### Kendala

## Soal 12

### Kendala

## Soal 13

### Kendala
