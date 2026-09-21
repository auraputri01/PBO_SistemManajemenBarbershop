Sistem Manajemen Barbershop

Mini Project Praktikum Pemrograman Berorientasi Objek (PBO)

Nama: Aura Putri Anandita Syarif NIM: 2509116094 Program Studi: Sistem Informasi

==============================================================================

Tentang Program Ini

Program ini adalah aplikasi konsol (tampilannya di terminal, tanpa GUI) yang saya buat dengan Java untuk membantu mengurus kegiatan di sebuah barbershop. Lewat program ini, kita bisa mencatat data pelanggan dan barber, melihat daftar layanan, mengatur antrean, mencatat proses pelayanan, sampai pembayarannya.

Semua data disimpan sementara di ArrayList, jadi datanya hilang kalau program ditutup. Untuk tugas ini saya fokus ke penerapan konsep PBO, terutama inheritance (pewarisan).

==============================================================================

Kenapa Memilih Barbershop?

Di barbershop ada beberapa jenis orang yang punya data dasar yang sama, yaitu ID dan nama, tapi aturannya berbeda-beda:

- Pelanggan biasa tidak dapat diskon, sedangkan pelanggan member dapat diskon.
- Barber biasa punya batas jumlah pelanggan yang bisa ditangani, sedangkan barber senior bisa menangani lebih banyak, tapi setiap pelayanannya ada biaya tambahan.

Karena ada data yang sama dan ada yang beda, kasus ini pas untuk memakai inheritance. Data yang sama cukup ditulis sekali di class induk, lalu class turunannya tinggal menambahkan atau mengubah bagian yang berbeda.

==============================================================================

Cara Kerja Program

Begitu program dijalankan, kita akan masuk ke menu utama dengan pilihan berikut:

1. Kelola Pelanggan
2. Kelola Barber
3. Lihat Daftar Layanan
4. Pelayanan Pelanggan
5. Cek Status Pelanggan
6. Lihat Status Barber
7. Ringkasan Barbershop
8. Keluar

Kita memilih menu dengan mengetik angkanya, lalu menekan Enter.

Di bagian pelanggan dan barber, kita bisa menambah, melihat, mengubah, dan menghapus data (CRUD).

Untuk pelayanan, alurnya begini:

- Pelanggan yang sudah terdaftar memilih barber dan layanan.
- Sistem otomatis membuatkan ID pelayanan dan nomor antrean.
- Status awalnya Menunggu. Saat barber mulai mengerjakan, statusnya jadi Diproses, dan setelah selesai jadi Selesai.
- Setelah selesai, pelanggan bisa membayar dengan Tunai atau QRIS. Kalau pembayaran berhasil, status pembayaran berubah dari Belum Bayar menjadi Lunas.

==============================================================================

Struktur Project

Project ini dibagi menjadi tiga package.

Package Model berisi class-class utama yang menggambarkan data di barbershop. Isinya ada Orang, Pelanggan, PelangganMember, Barber, BarberSenior, Layanan, dan Pelayanan.

Package util berisi class bantuan. Validator dipakai untuk mengecek input yang dimasukkan pengguna, sedangkan Format dipakai untuk merapikan tampilan, misalnya mengubah angka menjadi format rupiah.

Package com.mycompany.sistemmanajemenbarbershop berisi Main.java, yaitu menu dan alur program yang dijalankan, serta SistemManajemenBarbershop.java yang dibuat otomatis oleh NetBeans.

==============================================================================

Hierarki Class

Class paling atas adalah Orang. Class ini abstract, artinya tidak dibuat objeknya secara langsung dan hanya dipakai sebagai dasar. Isinya data yang dimiliki semua orang di barbershop, yaitu ID dan nama.

Dari Orang ada dua turunan langsung:

Pelanggan, untuk pelanggan yang datang ke barbershop. Turunannya adalah PelangganMember, yaitu pelanggan yang mendapat diskon.
Barber, untuk tukang cukur yang melayani pelanggan. Turunannya adalah BarberSenior, yaitu barber yang kapasitasnya lebih besar dan menambahkan biaya pada setiap pelayanan.

Jadi ada dua jalur pewarisan. Jalur pertama: Orang → Pelanggan → PelangganMember. Jalur kedua: Orang → Barber → BarberSenior.

Layanan dan Pelayanan bukan turunan Orang. Layanan menyimpan jenis layanan, sedangkan Pelayanan mencatat satu kali proses pelayanan, dari antrean sampai pembayaran.

==============================================================================

Bagian Kode yang Menerapkan Inheritance
1. Orang sebagai class induk

Orang menyimpan id dan nama. Di dalamnya ada method getPeran() yang sengaja dibiarkan kosong (abstract). Artinya, setiap class turunan wajib menjelaskan sendiri perannya.

<img width="1292" height="635" alt="image" src="https://github.com/user-attachments/assets/cb993076-0217-4e3e-9a68-21032f0973ff" />

Konstruktornya dibuat protected supaya hanya class turunan yang bisa memakainya.

2. Pelanggan mewarisi Orang

<img width="1097" height="510" alt="image" src="https://github.com/user-attachments/assets/a046d8e0-7ba2-4436-ad25-456238db0a49" />

- extends Orang artinya Pelanggan otomatis punya id, nama, dan semua method dari Orang.
- super(idPelanggan, nama) memanggil konstruktor Orang, jadi ID dan nama tidak perlu diurus ulang.
- getPeran() wajib ditulis karena di Orang sifatnya abstract.
- super.tampilkanData() menampilkan data dasar dari Orang dulu, lalu ditambah data khusus pelanggan (nomor HP dan diskon).

3. PelangganMember mewarisi Pelanggan

Class ini menurunkan Pelanggan, yang sendirinya sudah turunan Orang. Jadi pewarisannya bertingkat. Bedanya dengan pelanggan biasa: member mendapat diskon.

4. Barber mewarisi Orang

<img width="818" height="458" alt="image" src="https://github.com/user-attachments/assets/b65dc8f0-decd-4b51-832b-4ed0e3677709" />
<img width="365" height="112" alt="image" src="https://github.com/user-attachments/assets/2cc885f0-0a2d-4e72-972c-90ee9d88ca80" />

Cara kerjanya sama seperti Pelanggan, hanya datanya berbeda: barber punya pengalaman, jumlah pelanggan aktif, dan status kehadiran.

5. BarberSenior mewarisi Barber

<img width="827" height="477" alt="image" src="https://github.com/user-attachments/assets/b86f2416-4cfb-4797-90be-a57e430d238d" />

BarberSenior hanya menulis ulang (override) bagian yang berbeda: kapasitasnya 7 pelanggan, biaya tambahannya Rp10.000, dan perannya "Barber Senior". Sisanya, seperti cara menghitung status barber dan cara menampilkan data, ikut dari Barber dan Orang, jadi tidak perlu ditulis ulang.

Efek yang terlihat

Karena getPeran() ditulis berbeda di tiap class, method tampilkanData() yang sama akan menampilkan hasil yang berbeda tergantung objeknya. Objek BarberSenior akan tampil sebagai "Barber Senior", objek Barber tampil sebagai "Barber", dan seterusnya. Ini yang disebut polymorphism.

==============================================================================

Dokumentasi Program

Screenshot disimpan di folder screenshots/.

Menu Utama

<img width="433" height="222" alt="image" src="https://github.com/user-attachments/assets/29944229-b206-4af0-9389-91094d0b6ae0" />

Kelola Pelanggan

<img width="320" height="190" alt="image" src="https://github.com/user-attachments/assets/68f8ae82-8d40-4751-aeba-913c9f90675a" />

Kelola Barber

<img width="310" height="216" alt="image" src="https://github.com/user-attachments/assets/3979fcc0-bc65-4a24-8440-e70f81f18e65" />

Daftar Layanan

<img width="443" height="162" alt="image" src="https://github.com/user-attachments/assets/bccef8c9-9fdf-4e32-9d86-9962d44b5bcf" />

Pelayanan Pelanggan

<img width="432" height="140" alt="image" src="https://github.com/user-attachments/assets/d30b9f28-22bf-4344-a97c-0ec2bdf7cd17" />

Status Barber

<img width="472" height="692" alt="image" src="https://github.com/user-attachments/assets/ed37508c-7599-4179-9ab8-7d3bf643ea9b" />

Ringkasan Barbershop

<img width="542" height="556" alt="image" src="https://github.com/user-attachments/assets/0bab2925-cf97-42d0-90d1-003f2d29868b" />

==============================================================================






