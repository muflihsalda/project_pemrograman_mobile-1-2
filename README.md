# project_pemrograman_mobile 1 - 2


Nama    : Muflih Salda Maulana

NIM     : 312410527

Kelas:  : I241E

Matakuliah : Pemograman Mobile 1

Dosen Pengampu : Donny Maulana, S.Kom., M.M.S.I.

## Tugas

1. Splash Screen (Deteksi location, Bendera, Say Hello/Selamat Datang sesuai lokasi daerah masing-masing)

<img width="281" height="237" alt="Cuplikan layar 2025-11-11 211824" src="https://github.com/user-attachments/assets/0d669a19-2674-4f65-93c3-31059cb91f3e" />


- Tampilan logo

Menampilkan logo aplikasi.

- Mendeteksi Lokasi

Ketika User sedang di indonesia tampilan ini akan berbahasa indonesia dan juga memunculkan lambang negaranya, begitupun sebaliknya jika user berada seperti di amerika, jepang, jerman dan lain-lain maka akan menampilkan bahasa dan lambang negara tersebut.

2. StoryBoard Project

<img width="2000" height="1414" alt="1" src="https://github.com/user-attachments/assets/1f33c106-4cb6-41cd-9696-9dca32f71a50" />



3. Mockup Project

<img width="2000" height="1414" alt="2" src="https://github.com/user-attachments/assets/e7c03bfa-22b1-4512-9f8e-0cf59b660633" />



4. UI (User Interface) Project

<img width="717" height="367" alt="revisi_UI" src="https://github.com/user-attachments/assets/f2237b86-d444-4a6d-87fb-48a12a1f0c1f" />


# Implementasi android studio
---
##  Penjelasan Kode Program

### MainActivity.java

`MainActivity` adalah **inti aplikasi** yang bertugas:

* Mengambil lokasi pengguna
* Menampilkan jam & zona waktu
* Mengambil jadwal sholat
* Menjadwalkan notifikasi adzan

---

### Inisialisasi Komponen

```java
private TextView txtLokasi, txtZona, txtJam;
private TextView txtSubuh, txtDzuhur, txtAshar, txtMaghrib, txtIsya;
```

Digunakan untuk menampilkan:

* Lokasi
* Zona waktu
* Jam real-time
* Jadwal sholat

---

### Permission

```java
Manifest.permission.ACCESS_FINE_LOCATION
Manifest.permission.POST_NOTIFICATIONS
```

Digunakan untuk:

* Mengakses GPS
* Menampilkan notifikasi adzan

Permission dicek saat aplikasi pertama kali dibuka.

---

### Pengambilan Lokasi

```java
fusedLocationClient.getLastLocation()
```

Fungsi ini:

* Mengambil latitude & longitude
* Menentukan kota dan negara
* Menjadi dasar pengambilan jadwal sholat

**Catatan:**
Fake GPS hanya mengubah koordinat, **zona waktu tetap mengikuti sistem HP**.

---

### Menampilkan Zona Waktu

```java
TimeZone.getDefault()
```

Zona waktu:

* WIB
* WITA
* WIT
* GMT+X

Diambil langsung dari **pengaturan sistem Android**, bukan GPS.

---

### Jam Real-Time

```java
Handler + postDelayed
```

Jam diperbarui **setiap 1 detik** dan mengikuti zona waktu sistem.

---

### Mengambil Jadwal Sholat

```java
https://api.aladhan.com/v1/timings
```

API digunakan untuk mendapatkan:

* Subuh
* Dzuhur
* Ashar
* Maghrib
* Isya

Jadwal ditampilkan dalam format `HH:mm`.

---

### Menjadwalkan Notifikasi Adzan

```java
WorkManager + OneTimeWorkRequest
```

Fitur:

* Notifikasi berjalan di background
* Tepat pada waktu sholat
* Tidak tergantung aplikasi terbuka

---

### Anti Notifikasi Dobel

```java
enqueueUniqueWork(...)
SharedPreferences
```

Mekanisme:

* Jadwal hanya dibuat **1x per hari**
* Jika sudah dijadwalkan → tidak dibuat ulang

---

## AdzanWorker.java

File ini:

* Dipanggil oleh WorkManager
* Menampilkan notifikasi
* Memutar suara adzan

Tidak ada tombol manual, semua **otomatis**.

## Tampilan Notifikasi bila sudah masuk waktu sholat

![WhatsApp Image 2026-01-19 at 20 28 16](https://github.com/user-attachments/assets/1fd30028-bc11-4a16-be61-d2f11df93a52)




---
## Hasil Tampilan Aplikasi

https://youtube.com/shorts/WE7kDkWm9oE?feature=share

https://youtube.com/shorts/kCZWVr-wZTA?feature=share 

---




## Link Vidio tampilan Spless screen dan prototype 

https://youtu.be/G6a6rZumr2Q?si=63cH7D6pzo6tI68i 

## Link figma

https://www.figma.com/proto/tGTBqAyhH065rvIyyv3Wyt/APK-pengingat-sholat?node-id=1-5&starting-point-node-id=45%3A36&t=8XAzPGXmL89dUKco-1


---
### Pemrograman Mobile2 

1. Update figma Untuk Menambahkan Fitur kalender hijriyah dan Juga AI untuk Memberikan Saran ibadah sunah yang tertera pada kolom event pahala 

<img width="642" height="474" alt="image" src="https://github.com/user-attachments/assets/9a3a9e9c-46cb-4c46-8e0f-d9afdf91b7a1" />

Link Prototype

https://www.figma.com/proto/tGTBqAyhH065rvIyyv3Wyt/APK-pengingat-sholat?node-id=169-285&t=EbbgREhMNNKu5fhq-1&scaling=scale-down&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=45%3A36 

2. Implementasi android Untuk Membuat Fitur kalender Hijriyah


