### Tugas 7 - Ionic Framework

Nama: Ahmad Rian Syaifullah  
NIM: H1D022010  
SHIFT BARU : D

# Cara Kerja Login

**A) Saat User Membuka Aplikasi:**

1. AutoLoginGuard mengecek status authentication
2. Jika sudah login sebelumnya (token tersimpan), diarahkan ke halaman home
3. Jika belum login, tetap di halaman login

**B) Proses Login:**

1. User mengisi username dan password
2. Saat tombol login ditekan, method `login()` dijalankan
3. Dilakukan validasi:

   - Cek apakah username dan password tidak kosong
   - Jika kosong, tampilkan notifikasi error

4. Jika validasi berhasil:

   ```typescript
   - Data username dan password dikirim ke server via AuthenticationService
   - Request POST ke endpoint login.php
   - Server melakukan:
     - Koneksi ke database MySQL
     - Query untuk cek username & password (password dalam MD5)
     - Mengembalikan response dengan format JSON
   ```

5. **Handling Response**  
   Response dari server akan ditangani sebagai berikut:

   - **Jika Login Berhasil (status_login = "berhasil")**:

     - Simpan token dan username ke local storage menggunakan `Capacitor Preferences`.
     - Update status autentikasi menjadi `true`.
     - Bersihkan form login.
     - Redirect user ke halaman home.

   - **Jika Login Gagal**:
     - Tampilkan notifikasi error sesuai dengan kondisi, misalnya jika password salah atau terjadi masalah koneksi.
