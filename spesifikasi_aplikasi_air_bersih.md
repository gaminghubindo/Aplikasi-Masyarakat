# Spesifikasi Sistem: Aplikasi Pelaporan Air Bersih

## 1. Latar Belakang dan Tujuan
Aplikasi ini dikembangkan sebagai solusi digital untuk membantu masyarakat yang berada di lingkungan dengan akses air bersih yang kurang layak atau bermasalah. Melalui platform ini, masyarakat dapat secara langsung menyuarakan permasalahan air di daerah mereka agar dapat ditindaklanjuti.

## 2. Aktor dan Hak Akses (Role-Based Access Control)
Sistem ini menggunakan tiga tingkatan peran utama. Secara arsitektur perangkat lunak, terutama jika menerapkan konsep Object-Oriented Programming (OOP), ketiga peran ini merupakan turunan (inheritance) dari satu entitas utama, misalnya kelas `Account`, di mana masing-masing peran memiliki method dan kapsulasi data tersendiri.

### A. User (Masyarakat)
Sebagai pelapor utama dalam sistem.
*   **Melengkapi Data Lokasi:** Sebelum membuat laporan, user diwajibkan memasukkan data alamat dan lokasi lengkap daerah masing-masing untuk pemetaan yang akurat.
*   **Membuat Laporan:** Mengirimkan pengaduan masalah air bersih disertai bukti visual (unggah foto) dan deskripsi kondisi di lapangan.
*   **Pusat Bantuan (Helpdesk):** Mengakses fitur bantuan atau berinteraksi dengan Admin jika mengalami kesulitan dalam menggunakan fungsi-fungsi aplikasi.

### B. Admin
Sebagai pengelola operasional harian dan layanan pelanggan.
*   **Manajemen Laporan:** Menerima, meninjau, dan mengelola status laporan yang masuk dari User.
*   **Dukungan Pengguna:** Menjawab pertanyaan dan memandu User (Masyarakat) yang belum memahami cara penggunaan aplikasi.

### C. Super Admin
Sebagai pemegang kendali penuh atas sistem dan infrastruktur aplikasi.
*   **Manajemen Admin (CRUD):** Memiliki hak eksklusif untuk menambahkan akun Admin baru, mengedit, atau menghapus akun Admin yang sudah ada.
*   **Sistem Monitoring & Testing:** Melakukan pengujian fungsionalitas aplikasi dan memegang kontrol tertinggi terhadap konfigurasi sistem.

## 3. Rekomendasi Struktur Data (Normalisasi Database)
Agar sistem berjalan dengan ringan, tidak mengalami duplikasi (redundansi), dan bebas dari anomali data saat laporan bertambah banyak, database perlu dirancang dengan prinsip normalisasi (misalnya hingga tahap 3NF):
1.  **Tabel Accounts:** Menyimpan kredensial login (ID, Username, Password, RoleID).
2.  **Tabel Profiles:** Menyimpan data diri pengguna. 
3.  **Tabel Locations:** Memisahkan data hierarki wilayah (Provinsi, Kota/Kabupaten, Kecamatan, Kelurahan, Detail Alamat) agar terstruktur dengan rapi dan terhubung ke profil user atau laporan.
4.  **Tabel Reports:** Menyimpan data pengaduan (ReportID, UserID, LocationID, Deskripsi, Tanggal, Status).
5.  **Tabel Evidences:** Menyimpan file/foto bukti pelaporan yang memiliki relasi (Foreign Key) ke Tabel Reports.
6.  **Tabel Support_Chats:** Menampung log percakapan antara User dan Admin untuk keperluan bantuan teknis.

## 4. Alur Kerja (User Flow) Pelaporan Singkat
1.  User melakukan pendaftaran dan melengkapi profil serta **Lokasi Lengkap**.
2.  User masuk ke menu "Buat Laporan Baru".
3.  User mengunggah foto bukti air kotor/bermasalah dan mengisi keterangan.
4.  Laporan terkirim dan masuk ke *Dashboard* Admin.
5.  Admin memverifikasi laporan tersebut.
6.  (Opsional) Jika user kebingungan di langkah 1-3, user menekan tombol "Bantuan" untuk chat dengan Admin.
