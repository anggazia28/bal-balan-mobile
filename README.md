# Tugas Individu PBP

## - Name : Angga Ziaurrohchman
## - NPM : 2406495943
## - Kelas : PBP E

## Link Dokumentasi Tugas
[Tugas 7](../../wiki/[README]-Tugas-Individu-7)
[Tugas 8](../../wiki/[README]-Tugas-Individu-8)


### Jelaskan mengapa kita perlu membuat model Dart saat mengambil/mengirim data JSON? Apa konsekuensinya jika langsung memetakan Map<String, dynamic> tanpa model (terkait validasi tipe, null-safety, maintainability)?
Kita perlu membuat Dart Models saat mengambil atau mengirim data JSON untuk meningkatkantype safety, null-safety, dan kemudahan pemeliharaan.

Jika langsung dipetakan tanpa model maka akan mengakibatkan beberapa masalah/ketidakefisienan seperti 
- harus casting type data dan beresiko salah sehingga crash
- harus cek apakah value nya null atau tidak 
- harus mengubah/refactoring jika ada type data berubah

### Apa fungsi package http dan CookieRequest dalam tugas ini? Jelaskan perbedaan peran http vs CookieRequest.
Package http adalah paket standar Dart/Flutter untuk melakukan panggilan HTTP (seperti GET, POST, PUT, DELETE). Ini menyediakan klien dasar untuk berinteraksi dengan server web, menangani pembuatan permintaan, pengiriman data, dan penerimaan respons.

CookieRequest (biasanya bagian dari package lain seperti http_interceptor atau implementasi custom) adalah kelas yang memperluas fungsionalitas klien HTTP dasar untuk secara otomatis mengelola session cookies.

Perbedaan keduanya adalah 
- http hanya request http dasar sedangkan cookierequest sekaligus mengelola cookies
- http tidak otomatis menyimpan cookies yang diterima dari respon server sedangkan cookierequest otomatis
- http menyediakan method dasar sedangkan cookierequest hanya wraper atau interceptor

### Jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
Instance CookieRequest atau client HTTP yang berfungsi mengelola cookies perlu dibagikan (shared) ke semua komponen di aplikasi Flutter karena cookies (terutama sessionid dari Django) adalah penyimpan keadaan sesi (session state). Jika setiap komponen yang ingin melakukan panggilan API (misalnya, Service untuk data produk, Service untuk data pengguna) membuat instance klien HTTP baru, instance tersebut tidak akan memiliki akses ke session cookie yang didapatkan saat proses login. Akibatnya, setiap request yang dikirim oleh instance baru akan dianggap tidak terautentikasi oleh server Django, karena kunci sesi yang valid tidak ikut terlampir. Dengan membagikan satu instance CookieRequest melalui mekanisme seperti Dependency Injection (contohnya menggunakan Provider atau GetIt), kita memastikan bahwa client tersebut adalah sumber kebenaran tunggal yang secara persisten menyimpan, memperbarui, dan melampirkan session cookie ke semua panggilan API, sehingga menjaga sesi pengguna tetap aktif dan konsisten di seluruh aplikasi.

### Jelaskan konfigurasi konektivitas yang diperlukan agar Flutter dapat berkomunikasi dengan Django. Mengapa kita perlu menambahkan 10.0.2.2 pada ALLOWED_HOSTS, mengaktifkan CORS dan pengaturan SameSite/cookie, dan menambahkan izin akses internet di Android? Apa yang akan terjadi jika konfigurasi tersebut tidak dilakukan dengan benar?
Untuk memungkinkan Flutter (berjalan di emulator/perangkat seluler) berkomunikasi dengan Django (berjalan di lingkungan pengembangan lokal), beberapa konfigurasi spesifik diperlukan seperti pada ALLOWED HOST django, CORS django, SameSite, 

Jika tidak maka dapat terjadi kegagalan koneksi dan komunikasi seperti dissalowed host, bad request, django menolak mengirim respon, session cookie tidak disimpan oleh klien http flutter

### Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
Mekanisme pengiriman data dari input pengguna di Flutter hingga ditampilkan kembali adalah proses end-to-end yang melibatkan interaksi klien-server seperti 
- Input pengguna yang memasukan data melalui widget dan disimpan
- Data dikirimkan dengan dikonversikan menjadi JSON string  lalu membuat request POST ke API
- Django menerima request POST lalu memvalidasi data 
- Django merespon/menerima 
- JSON diurai kembali sesuai data type atau var
- Data dikonversikan ke model di tampilan flutter


### Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
Proses autentikasi adalah sebuah alur komunikasi yang memastikan identitas pengguna dari Flutter (klien) dikenali dan dipertahankan oleh Django (server), menggunakan Session Cookies sebagai kunci identifikasi.

Registrasi (Register)

Pengguna memulai dengan menginput data akun baru (nama pengguna, email, kata sandi) pada form registrasi di Flutter. Data ini kemudian dikumpulkan dan dikemas menjadi format JSON oleh klien Flutter. Flutter mengirimkan permintaan POST yang membawa JSON data tersebut ke endpoint registrasi yang telah disiapkan di Django. Di sisi Django, view yang menangani registrasi akan menerima request, mengurai JSON, memvalidasi data, dan jika valid, membuat instance pengguna baru di database dengan password yang telah di-hash. Django kemudian merespons dengan status sukses (biasanya HTTP 201 Created).

Masuk (Login)

Setelah berhasil mendaftar atau langsung ke menu login, pengguna menginput kredensial (nama pengguna/email dan kata sandi). Sama seperti registrasi, Flutter mengirimkan data ini melalui permintaan POST ke endpoint login Django. Django menerima request, memverifikasi kredensial terhadap data hash di database. Jika kredensial cocok, Django akan membuat session baru untuk pengguna tersebut di database dan menginstruksikan klien (Flutter) untuk menyimpan kunci sesi tersebut. Instruksi ini dilakukan melalui header Set-Cookie yang disertakan dalam respons sukses (HTTP 200 OK). Klien HTTP di Flutter (CookieRequest) secara cerdas menangkap header ini dan menyimpan session cookie tersebut secara internal. Setelah session cookie berhasil disimpan, Flutter memperbarui status autentikasi (misalnya, melalui State Management seperti Provider) menjadi terautentikasi, yang kemudian secara otomatis memicu navigasi dan menampilkan menu atau halaman utama aplikasi.

Akses Terautentikasi dan Keluar (Logout)

Setelah login berhasil, untuk setiap permintaan API berikutnya (misalnya, mengambil data profil, mengirim data), CookieRequest secara otomatis mengambil session cookie yang telah disimpan dan melampirkannya di header Cookie pada setiap request yang dikirim ke Django. Django menggunakan cookie ini untuk mengidentifikasi sesi dan pengguna, sehingga mengizinkan akses ke endpoint yang dilindungi. Ketika pengguna memilih logout, Flutter mengirimkan request ke endpoint logout Django. Django menerima request, menghancurkan atau mengakhiri sesi yang terkait di database, dan merespons sukses. Sebagai langkah terakhir, klien Flutter juga menghapus session cookie yang tersimpan dan memperbarui status autentikasi menjadi tidak terautentikasi, membawa pengguna kembali ke halaman login.

### Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).