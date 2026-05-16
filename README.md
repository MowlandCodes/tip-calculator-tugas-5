# Tugas 5 - Mobile Programming (Unit Test & Instrumentation Test)
Dokumentasi ini disusun untuk memenuhi kriteria penilaian pada mata kuliah Pemrograman Perangkat Bergerak. Project ini berfokus pada implementasi pengujian otomatis menggunakan framework Jetpack Compose, guna memastikan integritas fungsionalitas dan kualitas antarmuka pengguna pada aplikasi **Tip Time**.

## Infrastruktur Pengujian
Dalam proyek ini, diterapkan dua lapisan pengujian fungsional untuk menjamin akurasi kalkulasi serta stabilitas interaksi pengguna. Strategi ini mengadopsi prinsip keamanan berlapis guna memitigasi risiko kesalahan logika pada tahap produksi.

### Pengujian Unit Lokal (Validasi Logika Bisnis)
Lokasi berkas: `app/src/test/java/com/example/tiptime/TipCalculatorTests.kt`

Pengujian unit dijalankan pada lingkungan Java Virtual Machine (JVM) lokal. Fokus utama dari pengujian ini adalah memastikan fungsi `calculateTip()` memberikan luaran yang akurat berdasarkan parameter input yang diberikan.

#### Test Case 1: `calculateTip_20PercentNoRoundup` (Codelab)
**Deskripsi**: Memvalidasi akurasi kalkulasi tip dasar sebesar 20% tanpa fitur pembulatan.

**Skenario**: Nominal tagihan $10, persentase tip 20%, fitur pembulatan dinonaktifkan.

**Hasil yang Diharapkan**: `$2.00`.

#### Test Case 2: `calculateTip_20PercentRoundup` (Implementasi Mandiri)

**Deskripsi**: Memastikan fungsi pembulatan nilai ke atas (`round up`) beroperasi sesuai spesifikasi teknis untuk mencegah ketidaksinkronan data keuangan.

**Skenario**: Nominal tagihan $10, persentase tip 20%, fitur pembulatan diaktifkan.

**Hasil yang Diharapkan**: `$2.00` (Memastikan nilai bulat tetap konsisten dan tidak mengalami kesalahan presisi desimal).

### Pengujian Instrumentasi / UI (Interaksi Pengguna)
Lokasi berkas: `app/src/androidTest/java/com/example/tiptime/TipUITests.kt`

Pengujian ini mensimulasikan interaksi pengguna secara nyata pada perangkat atau emulator Android. Hal ini dilakukan untuk memastikan bahwa komponen antarmuka dapat merespons input secara tepat.

#### Test Case: `calculate_20_percent_tip`
**Prosedur Pengujian**:
- Memasukkan nilai `10` pada kolom input "Bill Amount". 
- Memasukkan nilai `20` pada kolom input "Tip Percentage". 
- Verifikasi: Memastikan komponen teks di layar menampilkan hasil kalkulasi akhir secara tepat, yakni `Tip Amount: $2.00`. 
- Tujuan: Menjamin stabilitas manajemen state pada Jetpack Compose dan memastikan tidak terjadi kegagalan sistem (crash) saat proses entri data.

