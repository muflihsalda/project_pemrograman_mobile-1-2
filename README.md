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

2. Implementasi android Untuk Membuat Fitur Kalender Hijriyah & Event Pahala

Fitur ini merupakan sistem kalender interaktif yang menyelaraskan penanggalan Masehi dengan Hijriyah secara real-time. Selain sebagai penunjuk tanggal, fitur ini berfungsi sebagai pengingat ibadah sunnah (Event Pahala) yang dihitung secara dinamis berdasarkan algoritma penanggalan Islam.

Fungsionalitas Utama
Dual-Calendar Synchronization: Menampilkan penanggalan Masehi dan Hijriyah secara berdampingan dalam satu tampilan grid yang intuitif.

Dynamic Event Detection (Event Pahala): Secara otomatis mendeteksi dan menandai hari-hari istimewa untuk beribadah, seperti:

Puasa Senin-Kamis: Mendeteksi nama hari dari setiap tanggal Masehi.

Puasa Ayyamul Bidh: Mendeteksi tanggal 13, 14, dan 15 pada setiap bulan Hijriyah (dengan pengecualian pada hari Tasyrik di bulan Dzulhijjah).

Monthly Navigation: Memungkinkan pengguna untuk melihat data penanggalan pada bulan-bulan sebelumnya atau yang akan datang dengan pembaruan data yang sinkron.

Implementasi Teknis
REST API Integration: Mengonsumsi data dari Aladhan API (gToHCalendar) menggunakan library Volley untuk mendapatkan pemetaan tanggal Masehi ke Hijriyah dalam format JSON.

Custom Grid Adapter: Implementasi CalendarAdapter untuk mengatur logika visual kalender, termasuk perhitungan offset hari agar tanggal satu dimulai pada kolom hari yang tepat (Sunday-Saturday).

Data Parsing & Logic Filtering:

Mengolah struktur data JSON yang kompleks untuk mengekstraksi nama bulan Hijriyah, tahun, dan informasi hari.

Menggunakan logika kondisional di dalam fungsi checkEvent untuk menentukan jenis ibadah sunnah yang relevan pada tanggal tertentu.

Reactive UI Updates: Menggunakan notifyDataSetChanged() pada RecyclerView dan GridView untuk memastikan antarmuka diperbarui seketika setelah data dari internet berhasil diunduh.

Alur Kerja (Workflow)
Request: Aplikasi mengirim permintaan ke API Aladhan berdasarkan bulan dan tahun yang sedang ditampilkan di UI.

Processing: Data JSON diterima dan diurai (parsing) untuk mengisi daftar calendarDays (untuk tampilan grid) dan eventPahalaList (untuk daftar kegiatan ibadah).

Validation: Sistem mengecek setiap tanggal apakah memenuhi kriteria ibadah sunnah tertentu.

Rendering: Data ditampilkan ke pengguna; tanggal yang memiliki "Event Pahala" diberikan penanda visual khusus pada kalender.


<img width="1267" height="643" alt="image" src="https://github.com/user-attachments/assets/fcd70129-d286-46cf-9227-61c75e42fa40" />

3. Membuat Fitur AI Sunnah Plener

AI Sunnah Planner adalah fitur asisten cerdas yang terintegrasi di dalam aplikasi pengingat ibadah untuk memberikan rekomendasi aktivitas sunnah secara personal. Fitur ini memanfaatkan Large Language Model (LLM) melalui Gemini AI API untuk mengonversi data mentah kalender menjadi pesan motivasi yang kontekstual.

Core Functionalities
Context-Aware Recommendations: AI menganalisis data harian dari API Aladhan (seperti Puasa Senin-Kamis atau Puasa Ayyamul Bidh) dan menghasilkan pengingat yang spesifik berdasarkan jenis ibadah tersebut.

Natural Language Generation: Mengubah notifikasi kaku menjadi percakapan yang hangat dan manusiawi, sehingga meningkatkan pengalaman pengguna (User Experience).

Personalization: AI menggunakan nama pengguna dan data waktu lokal untuk memberikan instruksi yang relevan, seperti saran persiapan sahur jika terdeteksi adanya jadwal puasa sunnah untuk keesokan harinya.

Technical Implementation
Large Language Model: Menggunakan model gemini-1.5-flash untuk pemrosesan teks yang cepat dan efisien pada perangkat mobile.

Prompt Engineering: Implementasi teknik prompting pada class GeminiAIHelper.java untuk memastikan output AI tetap berada dalam koridor islami, santun, dan informatif dengan batasan panjang kalimat tertentu.

Asynchronous Processing: Panggilan API dilakukan secara asinkron menggunakan ListenableFuture (Google Guava) untuk memastikan antarmuka aplikasi (UI Thread) tetap responsif dan tidak mengalami freezing saat AI sedang memproses teks.

Secure API Management: Keamanan kunci akses (API Key) dikelola menggunakan file local.properties yang diintegrasikan melalui BuildConfig untuk mencegah kebocoran kredensial pada repositori publik.

Workflow
Data Fetching: Aplikasi mengambil data kalender Hijriah dari API Aladhan.

Logic Filtering: Sistem menyaring event sunnah yang tersedia di bulan tersebut.

AI Processing: Data event terdekat dikirim sebagai parameter ke Gemini AI.

UI/UX Delivery: Output teks dari AI ditampilkan secara dinamis pada CardView khusus di dalam halaman kalender Hijriah.
