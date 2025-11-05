# Tugas Individu PBP

## - Name : Angga Ziaurrohchman
## - NPM : 2406495943
## - Kelas : PBP E

## Link Dokumentasi Tugas



### Jelaskan apa itu widget tree pada Flutter dan bagaimana hubungan parent-child (induk-anak) bekerja antar widget

Widget Tree adalah struktur hierarki berbentuk pohon yang menggambarkan susunan widget di Flutter. Setiap widget bisa memiliki parent (induk) dan children (anak).

Child berada didalam Parent sehingga parent akan mengatur gaya, tata letak, dan posisi child sementara child akan menentukan isi dari tampilannya. 
### Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya
* MaterialApp = Menjadi wrapper dari seluruh aplikasi agar menggunakan gaya material design dan mengatur navigasi, tema, route.
* Scaffold = Struktur utama halaman
* AppBar = Bar dibagian atas (hampir mirip seperti navbar) untuk judul dan action
* Column/Row = Membuat widget menjadi menggunakan aturan kolom dan baris yang bisa diatur (children)
* Container = Mengatur ukuran, margin, padding, warna, dan dekorasi
* Text = Text di layar
* ElevateButton = Tombol dengan gaya material design
* Navigator =Mengatur perpindahan antar halaman
* MediaQuery = Informasi ukuran layar dan device
* Icon = Icon
* InkWell = Area responsif touch
* Center = Membuat child berada di tengah
* GridView.count = Menampilkan children dalam grid dengan jumlah kolom tetap
* Expanded = Mengisi ruang yang bisa diisi (akan melebar sesuai free space)

### Apa fungsi dari widget MaterialApp? Jelaskan mengapa widget ini sering digunakan sebagai widget root
* Mengimplementasikan Material Design dari Google
* Mengatur tema aplikasi (colors, typography, shapes)
* Menyediakan navigasi dan routing
* Mengatur title aplikasi
* Mengelola Navigator untuk perpindahan halaman

MaterialApp sering digunakan sebagai widget root karena sudah menyediakan Navigator, Tema, MediaQuery dll sehingga lebih mudah. MaterialApp juga memiliki design yang sesuai standar dan familiar, Hot reload berkerja optimal, debugging mudah, dan memiliki konsistensi tinggi.

### Jelaskan perbedaan antara StatelessWidget dan StatefulWidget. Kapan kamu memilih salah satunya?

StatelessWidget tidak bisa diubah setelah dibuat sementara StatefulWidget dapat berubah saat runtime karena StatefulWidget punya state yang bisa diupdate. Akan tetapi StatelessWidget lebih ringan daripada StatefulWidget.

Jika widget hanya menampilkan data statis yang tidak berubah, maka lebih baik memakai StatelesWidget akan tetapi jika membutuhkan tracking user interaction seperti button click, input form maka StatefulWidget lebih baik digunakan. 

### Apa itu BuildContext dan mengapa penting di Flutter? Bagaimana penggunaannya di metode build?

BuildContext adalah referensi ke lokasi widget di tree yang mana setiap widget punya BuildContextnya sendiri. Ini digunakan untuk navigasi ke atas atau bawah widget tree. 

BuildContext penting karena dengan method method yang ada dapat memberikan akses ke tema, mediaquery, navigation, snackbars dll.

### Jelaskan konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart".

Hot Reload mempertahankan state aplikasi dan hanya rebuild widget tree dengan kode baru. Ini dipakai ketika kita ingin mengubah UI, logic dalam suatu method, hapus widget dll. Akan tetapi tidak dapat reload perubahan di main atau global var. 

Sementara Hot Restart merestart app dari awal dan semua state hilang. Karena itulah hot restart akan lebih lama, dan merebuild seluruh aplikasi dari main. Ini digunakan ketika kita ingin mengubah main function, mengubah global var, dan initState yang perlu reset state. 
