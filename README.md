# Jarkom-Modul-1-E19-2023
Laporan Resmi Praktikum Modul 1 Kelompok E19
| Nama               |  NRP       | 
|--------------------|-------------|
| M. Armand Giovanni | 5025211054  |
| Afiq Fawwaz Haidar | 5025211246  |

## Soal 1
**User melakukan berbagai aktivitas dengan menggunakan protokol FTP. Salah satunya adalah mengunggah suatu file.**
- **Sequence number (raw) berapa yang menunjukkan aktivitas ini pada paket?**
- **Acknowledge number (raw) berapa yang menunjukkan aktivitas ini pada paket?**
- **Sequence number (raw) berapa yang menunjukkan respons dari aktivitas ini pada paket?**
- **Acknowledge number (raw) berapa yang menunjukkan respons dari aktivitas ini pada paket?**

Gunakan _expression filter_ `ftp` pada _display filter_ untuk memunculkan paket dengan protokol `FTP`. berikutinya mencari paket data yang menggunakan perintah STOR, yaitu perintah yang digunakan untuk mengunggah suatu file, didapatkan yaitu nomor paket 147. Pada `packet detail pane` , buka _dropdown_ `TCP` atau `Transmission Control Protocol`. Terdapat `Sequence number (raw)` dan `Acknowledge number (raw)` dari paket.

![Request](images/1-stor.png)

Selanjutnya, kita buka paket yang merupakan `response` dari paket 147. Paket tersebut mengandung `.zip` yang sama dengan paket 147, terletak pada paket 149. Kita ulangi hal yang sama untuk memperoleh `Sequence number (raw)` dan `Acknowledge number (raw)` dari paket.

![Response](images/1-response.png)

Flag diperoleh sebagai berikut.

![Flag 1](images/flag-1.png)

## Soal 2
**Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer!**
**gunicorn**

Filter packet dengan query http kemudian follow menggunakan HTTP Stream. Pada bagian server terdapat informasi mengenai web server yang digunakan.

Flag diperoleh sebagai berikut.

![Flag 2](images/flag-2.png)

## Soal 3
**Dapin sedang belajar analisis jaringan. Bantu Dapin dengan hal berikut:**
- **Berapa banyak paket yang ter-capture dengan IP source atau destination address adalah `239.255.255.250` dan port `3702`?**
    **21**
- **Protokol lapisan transport apa yang digunakan?**
    **UDP**

> Filter packet dengan query `(ip.src == 239.255.255.250 and udp.port == 3702) or (ip.dst == 239.255.255.250 and udp.port == 3702)`. Pada bagian info terdapat informasi mengenai jumlah paket yang ter-capture. Pada bagian protokol terdapat informasi mengenai protokol lapisan transport yang digunakan.

Flag diperoleh sebagai berikut.

![Flag 3](images/flag-3.png)

## Soal 4
**Berapa nilai checksum yang didapat dari header pada paket nomor `130`?**

Nilai checksum dapat dilihat pada `packet detail pane` dari protokol `UDP`. Protokol yang digunakan paket 130 adalah `QUIC` sehingga harus dilakukan _decode_ terlebih dahulu sehingga dapat diubah menjadi `UDP` atau `User Datagram Protocol`.

![Decode Paket](images/4-decodeAs)

Setelah itu, pada `packet detail pane` dapat dibuka _dropdown_ dari `UDP` sehingga nilai _checksum_ dapat dilihat.

![Checksum Paket](images/4-checksum)

Flag diperoleh sebagai berikut.

![Flag 4](images/flag-4.png)


## Soal 5
**Elshe menemukan sebuah file packet capture yang menarik. Bantu Elshe untuk menganalisis file packet capture tersebut.**
- **Berapa banyak packet yang berhasil di-capture dari file pcap tersebut?**
> 60
- **Port berapa yang digunakan oleh server untuk layanan SMTP?**
> 25
- **Dari semua alamat IP yang ter-capture, IP berapakah yang merupakan alamat IP publik?**
> 74.53.140.153

> Setelah Membuka file .pcap menggunakan wireshark, kita dapat melihat jumlah paket yang ter-capture pada bagian info. 
> Untuk mengetahui port yang digunakan oleh server untuk layanan SMTP, kita dapat menggunakan filter `smtp` pada display filter. Setelah itu, kita dapat melihat port yang digunakan pada bagian info. 
> Untuk mengetahui alamat IP publik, kita dapat menggunakan filter `ip.src ` pada display filter. Setelah itu, kita dapat melihat alamat IP publik pada bagian info.

Flag diperoleh sebagai berikut.

![Flag 5](images/flag-5.png)

## Soal 6
**Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. Sebagai teman yang baik, ia selalu mengajak SlameT untuk bermain Valorant bersama. Suatu malam, terjadi sebuah hal yang tak terduga. Ketika Udin membuka game tersebut, laptopnya menampilkan sebuah field teks dan sebuah kode Invalid bertuliskan "server SOURCE ADDRESS 7812 is invalid". Ketika ditelusuri di Google, hasil pencarian hanya menampilkan "a1 e5 u21". Jiwa detektif SlameT pun bergejolak. Bantulah Udin dan SlameT untuk menemukan solusi kode error tersebut.**

## Soal 7
**Berapa jumlah packet yang menuju IP `184.87.193.88`?**

Setelah membuka _packet captured_, kita gunakan _filter expression_ `ip.dst == 184.87.193.88` yang merupakan filter paket dengan _destination IP_ `184.87.193.88`. Jumlah paket yang muncul dapat dijumlahkan.

![Display Filter](images/7-displayFilter.png)

Flag diperoleh sebagai berikut.

![Flag 7](images/flag-7.png)

## Soal 8
**Berikan kueri filter sehingga Wireshark hanya mengambil semua protokol paket yang menuju port `80`! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad).**
> tcp.dstport == 80 || udp.dstport == 80

Flag diperoleh sebagai berikut.

![Flag 8](images/flag-8.png)

## Soal 9
**Berikan kueri filter sehingga Wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat `10.39.55.34`!**

Setelah membuka _packet captured_, kita gunakan _filter expression_ `ip.src == 10.51.40.1 && ip.dst != 10.39.55.34`.
- `ip.src == 10.51.40.1` merupakan filter paket dengan _source IP_ `10.51.40.1`
- `ip.dst != 10.39.55.34` merupakan filter paket dengan negasi dari _destination IP_ `10.39.55.34`

Kedua _filter expression_ tersebut digabungkan dengan _logical operator_ `&&` atau `AND`

Flag diperoleh sebagai berikut.

![Flag 9](images/flag-9.png)

## Soal 10
**Sebutkan kredensial yang benar ketika pengguna mencoba login menggunakan Telnet.**
> dhafin:kesayangannyak0k0

> Pertama buka file .pcap menggunakan wireshark. Kemudian, kita dapat menggunakan filter `telnet` pada display filter. Setelah itu, kita follow TCP Stream pada salah satu paket. Pada bagian info, kita dapat melihat kredensial yang benar ketika pengguna mencoba login menggunakan Telnet. Untuk melihat kredensial yang benar, kita harus setiap packet yang terfilter menggunakan filter `telnet` pada display filter.

Flag diperoleh sebagai berikut.

![Flag 10](images/flag-10.png)
