# Jarkom-Modul-3-A03-2021

## Anggota

| Nama | NRP |
| :----: | :----: |
| Jessica Tasyanita | 05111940000043 |
| Daniel Sugianto | 05111940000075 |
| Ryan Fernaldy | 05111940000152 |

## Soal 1

### Kendala

## Soal 2

### Kendala

## Soal 3

### Kendala

## Soal 4

### Kendala

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

## Soal 6
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit. 
- Jipangu<br>
  Mengatur ``default-lease-time`` menjadi 360 detik (6 menit) untuk Switch1 dan 720 detik (12 menit) untuk Switch3. Mengatur ``default-lease-time``menjadi 7200 detik (120 menit) untuk Switch1 dan Switch3.
  ![image](https://user-images.githubusercontent.com/68326540/141312271-b3acde5c-46b4-4fa9-85f7-1c26bb5e6e7f.png)

- Loguetown (Switch1)<br>
  ![image](https://user-images.githubusercontent.com/68326540/141312003-a2d3db49-bcad-4f3e-a997-4ca382fba875.png)
- Tottoland (Switch3)<br>


### Kendala

## Soal 7
Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69 
### Kendala

## Soal 8
Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi. Pada Loguetown, proxy harus bisa diakses dengan nama jualbelikapal.yyy.com dengan port yang digunakan adalah 5000
### Kendala

## Soal 9
gar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu luffybelikapalyyy dengan password luffy_yyy dan zorobelikapalyyy dengan password zoro_yyy
### Kendala

## Soal 10
Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari Senin-Kamis pukul 07.00-11.00 dan setiap hari Selasa-Jum’at pukul 17.00-03.00 keesokan harinya (sampai Sabtu pukul 03.00)
### Kendala

## Soal 11

### Kendala

## Soal 12

### Kendala

## Soal 13

### Kendala
