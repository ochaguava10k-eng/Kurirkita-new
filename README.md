# KurirKita

Aplikasi driver pengantaran dibangun dari nol (clean-room), merek dan desain sendiri, untuk
dijadikan dasar proyek Android Anda sendiri. Dibuat dengan Kotlin + Jetpack Compose.

Proyek ini **tidak** menyalin kode, aset, atau logika dari aplikasi pengantaran mana pun, dan
**tidak** berisi mekanisme untuk mengelabui deteksi lokasi/GPS palsu atau pemeriksaan integritas
perangkat milik platform lain. Semua data (order, saldo, riwayat) adalah data contoh/dummy di
dalam aplikasi, belum terhubung ke server sungguhan.

## Fitur yang sudah ada

- **Login** (contoh/dummy, belum terhubung ke backend nyata).
- **Beranda**: sakelar online/offline, order aktif, dan order masuk dengan dialog hitung mundur.
- **Menu Nada Dering Order Masuk** (Beranda → ikon lonceng, atau Profil → "Nada Dering Order
  Masuk"): memilih nada dering lewat pemilih nada dering bawaan Android, tombol coba bunyikan,
  serta sakelar aktif/nonaktif untuk bunyi dan getar saat order masuk.
- **Riwayat Order**: daftar order yang pernah diselesaikan (data contoh).
- **Dompet**: saldo dan daftar transaksi (data contoh).
- **Profil**: info driver dan akses ke pengaturan nada dering.

## Build APK tanpa install apa pun (lewat GitHub)

Proyek ini sudah dilengkapi `.github/workflows/build-apk.yml` yang otomatis mem-build APK
lewat GitHub Actions setiap kali kode di-push ke branch `main`. Tidak perlu install Android
Studio atau Gradle di komputer Anda. Lihat panduan langkah demi langkah di percakapan, atau:

1. Buat akun & repository baru di github.com (public/private, kosong).
2. Upload semua isi folder proyek ini ke repository tersebut (commit ke branch `main`).
3. Buka tab **Actions** di repository → tunggu sampai proses selesai (tanda centang hijau).
4. Buka hasil run tersebut → bagian **Artifacts** → unduh `KurirKita-debug-apk`.
5. Ekstrak zip-nya, di dalamnya ada `app-debug.apk` — pindahkan ke HP dan install.

## Cara menjalankan (lewat Android Studio, opsional)

1. Install [Android Studio](https://developer.android.com/studio) versi terbaru.
2. Buka folder proyek ini di Android Studio (`File > Open`), biarkan Gradle sync berjalan
   (akan otomatis mengunduh Gradle wrapper sesuai `gradle/wrapper/gradle-wrapper.properties`).
3. Jalankan di emulator atau HP (`Run > Run 'app'`), minimum Android 7.0 (API 24).
4. Saat aplikasi pertama kali jalan, login dengan nomor HP ≥ 9 digit dan kata sandi ≥ 4 karakter
   (nilai apa saja yang memenuhi syarat ini akan diterima, karena ini hanya demo).
5. Di Beranda, aktifkan sakelar "Online" — order contoh akan muncul secara acak setiap
   8–18 detik lengkap dengan bunyi dan getar.

## Struktur proyek

```
app/src/main/java/com/kurirkita/app/
├── data/
│   ├── model/      Order, WalletTransaction, DriverProfile
│   ├── prefs/      RingtonePrefs (DataStore untuk preferensi nada dering)
│   └── repo/       OrderRepository, AuthRepository, WalletRepository (data contoh)
├── notification/   OrderNotificationHelper (channel, bunyi, getar)
└── ui/
    ├── theme/      Warna & tema Material3
    ├── navigation/ Routes & NavGraph
    ├── components/ BottomNavBar
    └── screens/    login, home, orders, wallet, profile, settings (nada dering)
```

## Langkah lanjutan yang disarankan

- Ganti `OrderRepository`, `AuthRepository`, `WalletRepository` dengan pemanggilan API nyata
  (mis. Retrofit) ke backend Anda sendiri.
- Tambahkan penyimpanan sesi login (DataStore/Token) agar tidak perlu login ulang setiap buka app.
- Tambahkan peta (Google Maps SDK) untuk rute pengantaran sungguhan.
- Tambahkan ikon aplikasi yang lebih matang (ikon dasar di `res/mipmap-xxxhdpi/` saat ini hanya
  placeholder sederhana).

## Lisensi & kepemilikan

Seluruh kode di proyek ini ditulis baru dan menjadi milik Anda untuk dikembangkan — silakan ubah
nama paket, merek, warna, dan logo sesuai kebutuhan sebelum dipublikasikan.
