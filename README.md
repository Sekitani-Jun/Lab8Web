## A. Identitas dan Capaian Praktikum

| | |
|---|---|
| **Nama** | Jumari |
| **NIM** | 312510077 |
| **Kelas** | I252A |
| **Mata Kuliah** | Pemrograman Web |
| **Nomor Modul** | 8 |
| **Topik** | CRUD menggunakan PHP |
| **Cakupan** | Sintaks PHP, MySQL |
| **Perangkat** | Laptop/PC, web browser, Visual Studio Code, PHP, dan server lokal Laragon, MySQL |

## B. Tujuan Praktikum

1. Mahasiswa mampu memahami konsep dasar Database.
2. Mahasiswa mampu memahami konsep dasar CRUD menggunakan PHP.
3. Mahasaswa mampu membuat program CRUD sederhana menggunakan PHP.

## C. Latihan

Struktur Folder:

```
C:\laragon\www\Lab8_php_database\
|
|--hapus.php
|--index.php
|--koneksi.php
|--style.css
|--tambah.php
|--ubah.php
```

### 1. Membuat Database Terlebih Dahulu

Masuk ke MySQL melalui Laragon,
![Buat database](media\1.png)

Buat Tabel
![Buat tabel](media\2.png)

Hasil
![Hasil struktur tabel](media\3.png)

### 2. Buka Direktori PHP

Koneksikan dengan Database. Buat file dengan nama koneksi.php

![Kode koneksi.php](media\4.png)

### 3. Membuat file index untuk menampilkan data

Buat file dengan nama index.php berdasarkan modul

Ikut menambahkan untuk fitur tambah barang

![Fitur tambah barang](media\5.png)

Juga menambahkan fitur ubah dan hapus berdasarkan id_barang

![Fitur ubah dan hapus](media\6.png)

Serta membuat file css untuk tampilan

![Kode style.css](media\7.png)

Hasil:

![Hasil tampilan data barang](media\8.png)

### 4. Menambahkan Data

- Menggunakan format tambah.php
- `error_reporting(E_ALL);` memerintahkan PHP untuk menampilkan semua jenis pesan kesalahan atau peringatan (*warning/notice*) agar mudah dilacak saat proses pengembangan.
- `include_once 'koneksi.php';` menyertakan file koneksi satu kali untuk mengaktifkan variabel `$conn` yang menghubungkan PHP dengan database MySQL.
- `if (isset($_POST['submit']))` memeriksa apakah tombol bernama submit sudah diklik oleh pengguna.
- `$filename = str_replace(' ', '_', $file_gambar['name']);` mengganti karakter spasi pada nama file menjadi garis bawah (_) agar alamat URL gambar tidak rusak saat dipanggil HTML.

![Kode tambah.php](media\9.png)

Serta menambahkan css untuk mempercantik

![CSS form tambah barang](media\10.png)

Hasil:

![Hasil form tambah barang](media\11.png)

### 5. Mengubah Data

Membuat file baru ubah.php

- `error_reporting(E_ALL);` Fungsi bawaan PHP untuk mengatur jenis kesalahan yang ditampilkan. Konstanta `E_ALL` memerintahkan PHP menampilkan seluruh jenis pesan kesalahan (*Fatal Error*, *Warning*, maupun *Notice*), sehingga memudahkan pelacakan *bug* saat kode diuji.
- `include_once 'koneksi.php';` Menyisipkan dan menjalankan isi file koneksi.php (agar variabel koneksi `$conn` dapat digunakan). Akhiran `_once` memastikan file tersebut hanya dipanggil satu kali dalam satu halaman untuk mencegah error pemanggilan ganda.
- `$id = $_POST['id'];` hingga `$stok = $_POST['stok'];` Mengambil nilai dari masing-masing elemen `<input>` atau `<select>` berdasarkan atribut name-nya, lalu menyimpannya ke dalam variabel lokal (`$id`, `$nama`, `$kategori`, `$harga_jual`, `$harga_beli`, `$stok`) agar lebih ringkas saat disusun ke dalam query SQL. Khusus `$_POST['id']` diambil dari input tersembunyi (`type="hidden"`) sebagai acuan ID barang yang akan diperbarui di database.

![Kode ubah.php](media\12.png)

Hasil: jika stok dirubah

![Hasil ubah stok](media\13.png)

Hasil: saat telah disimpan

![Hasil setelah disimpan](media\14.png)

### 6. Hapus Data

Membuat file baru hapus.php

- `include_once 'koneksi.php';` Memanggil file koneksi.php satu kali untuk mengaktifkan variabel `$conn` agar skrip ini dapat terhubung ke database MySQL.
- `$id = $_GET['id'];`
  - `$_GET` adalah variabel *superglobal* yang menangkap data yang dikirim melalui alamat URL.
  - Saat Anda mengeklik tautan `<a href="hapus.php?id=3">Hapus</a>` di index.php, angka 3 pada parameter `?id=3` akan ditangkap oleh `$_GET['id']` dan disimpan ke dalam variabel `$id`.
- `$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";` Menyusun perintah query SQL untuk menghapus data:
  - `DELETE FROM data_barang`: Perintah untuk menghapus baris data dari tabel data_barang.
  - `WHERE id_barang = '{$id}'`: Syarat penentu baris mana yang dihapus (hanya baris dengan kolom id_barang yang sesuai dengan nilai `$id`). Klausa WHERE ini sangat krusial—tanpanya, seluruh isi tabel akan terhapus.
- `$result = mysqli_query($conn, $sql);`
- `header('location: index.php');`

![Kode hapus.php](media\15.png)

Hasil: Menghapus HP OPPO Android

![Sebelum menghapus](media\16.png)

Hasil: Setelah dihapus

![Setelah dihapus](media\17.png)
