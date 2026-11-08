# Tugas-10
# MoneyTrack – Aplikasi Catatan Keuangan Pribadi

**Tugas P10 Pemrograman Mobile**  
Program Studi Sistem dan Teknologi Informasi  
Universitas Muhammadiyah Kotabumi

## Identitas
- Nama: Ananda Rizky Feryansyah
- NPM: 2459201003
- Kelas: 5 B
- Mata Kuliah: Pemrograman Mobile

## Deskripsi

MoneyTrack adalah aplikasi Android untuk membantu pengguna mencatat dan memantau keuangan pribadi. Aplikasi menyediakan fitur pencatatan pemasukan dan pengeluaran, pengelolaan transaksi, ringkasan saldo, statistik keuangan, serta pengaturan aplikasi.

Pada proyek ini, **SharedPreferences digunakan untuk menyimpan pengaturan pengguna**, sedangkan data transaksi disimpan menggunakan **SQLite**.

## Fitur Aplikasi

1. **Dashboard:** Menampilkan saldo, total pemasukan, total pengeluaran, dan transaksi terbaru.
2. **Transaksi:** Menambahkan, mengedit, menghapus, mencari, dan memfilter transaksi.
3. **Statistik:** Menampilkan ringkasan keuangan dan pengeluaran berdasarkan kategori.
4. **Pengaturan Pengguna:** Menyimpan nama pengguna, tema aplikasi, mata uang, dan status pengaturan notifikasi.
5. **Dark Mode dan Light Mode:** Menerapkan tema sesuai pilihan pengguna dan mempertahankannya ketika aplikasi dibuka kembali.

## Teknologi yang Digunakan

- Bahasa pemrograman: Java
- Tampilan aplikasi: XML Layout
- Penyimpanan preferensi: SharedPreferences
- Penyimpanan transaksi: SQLite
- AndroidX AppCompat
- Material Components
- RecyclerView
- ConstraintLayout
- Minimum Android: API 24 (Android 7.0)
- Compile SDK: 34
- Target SDK: 34

## Penerapan SharedPreferences

SharedPreferences diterapkan melalui class `PrefsManager.java` yang berada di:

`app/src/main/java/com/example/moneytrack/utils/PrefsManager.java`

Data pengaturan yang disimpan:

| Pengaturan | Key | Tipe Data | Nilai Awal |
|---|---|---|---|
| Nama pengguna | `user_name` | String | `Pengguna` |
| Tema aplikasi | `theme_mode` | Integer | Light Mode |
| Mata uang | `currency` | String | `IDR` |
| Status notifikasi | `notification_enabled` | Boolean | Aktif (`true`) |

### Method Utama PrefsManager

| Method | Kegunaan |
|---|---|
| `setUserName()` / `getUserName()` | Menyimpan dan membaca nama pengguna |
| `setThemeMode()` / `getThemeMode()` | Menyimpan dan membaca pilihan tema |
| `applyTheme()` | Menerapkan tema tersimpan ke aplikasi |
| `setCurrency()` / `getCurrency()` | Menyimpan dan membaca kode mata uang |
| `setNotificationEnabled()` / `isNotificationEnabled()` | Menyimpan dan membaca status pengaturan notifikasi |
| `saveSettings()` | Menyimpan seluruh pengaturan sekaligus |

Penyimpanan menggunakan `SharedPreferences.Editor` dan `apply()`. Method `apply()` memperbarui nilai preferensi dan menulisnya ke penyimpanan secara asynchronous.

### Alur Penerapan Tema

1. Pengguna membuka menu Pengaturan.
2. Pengguna memilih Dark Mode atau Light Mode.
3. Pengguna menekan Simpan Pengaturan.
4. `PrefsManager.saveSettings()` menyimpan pengaturan.
5. `PrefsManager.applyTheme()` menerapkan tema yang dipilih.
6. Ketika aplikasi dijalankan kembali, tema tersimpan dibaca dan diterapkan kembali.

**Catatan:** SharedPreferences pada proyek ini menyimpan pengaturan pengguna, bukan daftar transaksi keuangan.

## Penyimpanan Data Transaksi

Data transaksi dikelola oleh `DatabaseHelper.java` menggunakan SQLite. Database yang digunakan bernama `moneytrack.db` dengan tabel `transactions`.

Data transaksi mencakup jenis transaksi, nominal, kategori, deskripsi, dan tanggal. Operasi tambah, baca, ubah, dan hapus transaksi dilakukan melalui `DatabaseHelper`.

Dengan demikian:

- **SharedPreferences:** Menyimpan preferensi atau pengaturan pengguna.
- **SQLite:** Menyimpan data pemasukan dan pengeluaran.

## Struktur Folder Utama

```text
MoneyTrack/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/example/moneytrack/
│       │   ├── MainActivity.java
│       │   ├── MoneyTrackApp.java
│       │   ├── AddTransactionActivity.java
│       │   ├── adapter/
│       │   ├── database/
│       │   │   └── DatabaseHelper.java
│       │   ├── fragment/
│       │   │   ├── DashboardFragment.java
│       │   │   ├── TransactionFragment.java
│       │   │   ├── StatisticsFragment.java
│       │   │   └── SettingsFragment.java
│       │   ├── model/
│       │   ├── utils/
│       │   │   ├── PrefsManager.java
│       │   │   ├── CurrencyUtils.java
│       │   │   └── DateUtils.java
│       │   └── view/
│       └── res/
│           ├── drawable/
│           ├── layout/
│           ├── menu/
│           ├── values/
│           └── values-night/
├── gradle/
├── build.gradle
├── gradle.properties
├── settings.gradle
└── README.md
```

## Cara Menjalankan Proyek

1. Unduh atau clone repository ini.
2. Ekstrak proyek jika diunduh dalam bentuk ZIP.
3. Buka Android Studio.
4. Pilih File → Open, kemudian pilih folder proyek MoneyTrack yang berisi `settings.gradle`.
5. Tunggu proses Gradle Sync selesai.
6. Gunakan emulator Android dengan API 24 atau lebih baru, atau hubungkan perangkat Android melalui USB Debugging.
7. Klik Run untuk menjalankan aplikasi.

Android Studio mungkin perlu mengunduh komponen Gradle dan Android SDK yang sesuai. Koneksi internet diperlukan ketika komponen tersebut belum tersedia.

## Pengujian SharedPreferences

Untuk menguji apakah pengaturan benar-benar tersimpan:

1. Jalankan aplikasi MoneyTrack.
2. Buka menu Pengaturan.
3. Aktifkan Dark Mode.
4. Ubah nama pengguna jika diperlukan.
5. Tekan Simpan Pengaturan.
6. Tutup aplikasi dan lakukan Force Stop melalui pengaturan Android.
7. Buka kembali MoneyTrack.
8. Periksa apakah tema dan nama pengguna masih sesuai dengan pengaturan sebelumnya.

**Hasil yang diharapkan:** Pengaturan yang telah disimpan tetap digunakan setelah aplikasi dibuka kembali.

## Catatan

- Pengaturan notifikasi pada proyek ini menyimpan status pilihan pengguna. Penyimpanan preferensi tersebut tidak dengan sendirinya mengirim notifikasi.
- Kode mata uang bawaan adalah `IDR`.
- Data transaksi disimpan di SQLite, bukan SharedPreferences.
