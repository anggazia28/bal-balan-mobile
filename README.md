# Tugas Individu PBP

## - Name : Angga Ziaurrohchman
## - NPM : 2406495943
## - Kelas : PBP E

## Link Dokumentasi Tugas
[Tugas 7](../../wiki/[README]-Tugas-Individu-7)


### Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement() pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?

Navigator.push() akan menumpuk atau menambah halaman baru diatas halaman sebelumnya/saat ini, sehingga nanti dapat kembali ke halaman sebelumnya dengan Navigator.pop() atau tombol back
Navigator.pushReplacement() akan mengganti halaman saat ini dengan halaman baru dan halaman lama dihapus sehingga tidak dapat kembali ke halaman lama/sebelumnya

Halaman umum yang biasanya akan digunakan kembali seperti home, detail produk lebih baik menggunakan push tapi jika yang tidak perlu kembali lagi ke halaman tersebut seperti add product atau login maka lebih baik menggunakan pushReplacement

### Bagaimana kamu memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi?

Widget Scaffold digunakan sebagai kerangka utama setiap halaman agar memiliki struktur yang konsisten. Di dalamnya, AppBar berfungsi menampilkan judul dan ikon navigasi seperti keranjang, sedangkan Drawer digunakan sebagai menu navigasi samping untuk berpindah antar halaman seperti Home, Produk, dan Tentang Aplikasi

### Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti Padding, SingleChildScrollView, dan ListView saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.

Layout widget seperti Padding, SingleChildScrollView, dan ListView membantu tampilan form agar rapi, tidak menumpuk, dan bisa discroll saat layar kecil.
* Padding memberi jarak antar elemen supaya tidak terlalu rapat.
* SingleChildScrollView membuat seluruh form bisa di-scroll kalau isinya panjang.
* ListView mempermudah menampilkan daftar input atau produk dalam bentuk list yang fleksibel.

Contoh pada aplikasi
Padding di sekitar TextField agar jarak antar form rapi dan SingleChildScrollView agar form bisa di scroll saat keyboard muncul

### Bagaimana kamu menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko?

Mengatur ThemeData di widget MaterialApp, seperti primaryColor, colorScheme, dan scaffoldBackgroundColor.
Dengan begitu, semua elemen seperti AppBar, tombol, ikon, dan kartu produk menggunakan warna utama yang sama, sehingga aplikasi Bal balan punya identitas visual yang konsisten dan khas, sesuai brand toko.