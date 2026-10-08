# Cron Job Documentation

Dokumentasi sederhana mengenai penggunaan **Cron Job pada Linux** untuk menjalankan task secara otomatis berdasarkan jadwal tertentu.

## 📌 Apa itu Cron Job?

Cron Job adalah scheduler pada sistem Linux yang digunakan untuk menjalankan perintah secara otomatis pada waktu tertentu.

Format dasar:

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Hari dalam minggu
│ │ │ └──── Bulan
│ │ └────── Hari dalam bulan
│ └──────── Jam
└────────── Menit
```

Contoh:

```text
* * * * * command
```

Artinya command dijalankan **setiap menit**.

---

## 🔧 Melihat Cron

Untuk melihat cron yang sedang aktif:

```bash
crontab -l
```

---

## ➕ Menambahkan Cron Tanpa Menghapus Cron Lama

Gunakan:

```bash
(crontab -l 2>/dev/null; echo "CRON_BARU") | crontab -
```

Cara ini mengambil konfigurasi cron yang sudah ada kemudian menambahkan konfigurasi baru.

Contoh:

```bash
(crontab -l 2>/dev/null; echo "* * * * * wget -q URL -O /path/file.php") | crontab -
```

> **Catatan:** Pastikan command yang ditambahkan berasal dari sumber yang dipercaya.

---

## ⚠️ Menggunakan `echo | crontab -`

Contoh:

```bash
echo "* * * * * command" | crontab -
```

Cara ini berbeda dengan metode sebelumnya karena isi yang diberikan akan menjadi **crontab baru**. Konfigurasi cron sebelumnya dapat tergantikan.

Jika ingin mempertahankan cron lama, gunakan metode `crontab -l` + `echo` seperti pada bagian sebelumnya.

---

## 🗑️ Menghapus Cron Tertentu

Salah satu cara adalah memfilter baris berdasarkan kata tertentu:

```bash
crontab -l | grep -v "kata_kunci_cron" | crontab -
```

Setelah melakukan perubahan, periksa kembali:

```bash
crontab -l
```

---

## 📥 Contoh Penggunaan `wget`

Cron dapat digunakan untuk menjalankan `wget` secara berkala:

```bash
* * * * * wget -q URL -O /path/tujuan/file
```

Keterangan:

- `wget` → mengambil resource dari URL
- `-q` → mode quiet
- `-O` → menentukan lokasi/nama file output
- `* * * * *` → menjalankan command setiap menit

---

## 🔐 Security Notes

Cron yang mengambil file dari internet dan menulis langsung ke direktori web harus digunakan dengan hati-hati.

Sebelum menjalankan cron:

1. Pastikan URL berasal dari sumber yang dipercaya.
2. Periksa isi file sebelum deployment.
3. Hindari menjalankan file dengan hak akses berlebihan.
4. Jangan mengekspos web console atau shell ke publik.
5. Gunakan version control dan proses deployment yang terkontrol.

---

## 📚 Tujuan Repository

Repository ini dibuat sebagai dokumentasi dan referensi penggunaan **Cron Job Linux**, khususnya untuk memahami:

- konfigurasi crontab
- penambahan cron
- penghapusan cron
- penjadwalan command
- penggunaan `wget` dalam cron
- dasar keamanan Cron Job

> **Disclaimer:** Gunakan contoh konfigurasi hanya pada server dan sistem yang kamu miliki atau memiliki izin untuk kelola.
