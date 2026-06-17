# 📑 Dokumentasi & History Prompting - UAS Grafika Komputer

## 👤 Informasi Mahasiswa
* **Nama:** Raymond Indrawan Wijaya
* **Program Studi:** S1 Informatika
* **Asal Institusi:** STTS Surabaya
* **Mata Kuliah:** Grafika Komputer (Genap 2025/2026)
* **Tanggal Pengerjaan:** 17 Juni 2026

---

## 🛠️ Aplikasi 1: Lambertian Diffuse Reflection (Soal 1)
Aplikasi pertama merupakan visualizer interaktif berbasis web yang mensimulasikan pencahayaan klasik **Lambertian Diffuse Reflection** pada permukaan segitiga 3D dinamis tanpa menggunakan komponen Generative AI pada runtime aplikasi hasil akhir.

* **Live Demo URL:** [https://unreturnity.github.io/uas-grafika/](https://unreturnity.github.io/uas-grafika/)
* **File Kerja:** `index.html`

### Fitur Utama Soal 1:
1. **Interactive 3D Viewport:** Menggunakan library `Three.js` klasik untuk me-render bidang segitiga koordinat input secara *real-time* lengkap dengan indikator vektor normal ($\vec{N}$) warna biru dan vektor arah cahaya ($\vec{L}$) warna kuning.
2. **Dynamic Vertex Control:** Pengguna dapat mengubah koordinat kartesian ($X, Y, Z$) untuk ketiga sudut segitiga ($A, C, E$) secara manual untuk merubah bentuk geometri secara instan.
3. **Automated KaTeX Step-by-Step:** Menampilkan seluruh urutan kalkulasi linear matematika secara transparan seolah ditulis manual di atas kertas menggunakan formatting `KaTeX`. Setiap kali slider atau input diubah, angka di dalam langkah rumus ikut berhitung otomatis secara dinamis.

---

## 🛠️ Aplikasi 2: Camera Matrix Configuration Simulator (Soal 2)
Aplikasi kedua merupakan simulator interaktif mandiri yang digunakan untuk menyusun, menghitung, dan memvisualisasikan matriks transformasi kamera (View Matrix dan Perspective Projection Matrix) dari konfigurasi ruang 3D global secara instan.

* **Live Demo URL:** [https://unreturnity.github.io/uas-grafika/camera.html](https://unreturnity.github.io/uas-grafika/camera.html)
* **File Kerja:** `camera.html`

### Fitur Utama Soal 2:
1. **Camera Rig Representation:** Memvisualisasikan posisi fisik kamera (koordinat Eye $E$) sebagai box wireframe biru dan titik fokus bidikan (Target $T$) sebagai sphere merah, lengkap dengan visualisasi garis batas ruang pandang (*View Frustum Lines*) berwarna cyan yang merespon perubahan secara langsung.
2. **Complete Optics Parameter Controls:** Slider interaktif untuk mengubah sudut pandang (*Field of View / FOV*), aspek rasio layar, perputaran arah tegak (*Up-Vector Tilt Angle*), serta ambang batas jarak rendering (*Near* dan *Far Clipping Planes*).
3. **Real-time Matrix Generation:** Menghasilkan breakdown matematis murni untuk matriks transformasi pandangan dimensi $4 \times 4$ ($M_{view}$) menggunakan perhitungan koordinat basis vektor ($\vec{u}, \vec{v}, \vec{n}$) dan elemen penskalaan proyeksi perspektif ($M_{proj}$) secara dinamis tanpa jeda.

---

## 🛠️ Aplikasi 3: Raytracing & Inverse Transformation Simulator (Soal 3)
Aplikasi ketiga merupakan simulator interaktif mandiri yang mensimulasikan pencarian titik tabrakan antara garis lurus ray dengan objek bola primitif yang mengalami transformasi non-uniform (Translasi dan Penskalaan / Scaling).

* **Live Demo URL:** [https://unreturnity.github.io/uas-grafika/raytrace.html](https://unreturnity.github.io/uas-grafika/raytrace.html)
* **File Kerja:** `raytrace.html`

### Fitur Utama Soal 3:
1. **Global Raytrace Viewport:** Memvisualisasikan lintasan penembakan garis sinar (*Ray Trajectory Vector*) berwarna oranye menuju objek bola (*Target Sphere Mesh*) berwarna ungu yang posisinya dapat digeser dan ukurannya dapat ditarik secara dinamis.
2. **Inverse Transformation Vector Shifting:** Menampilkan matriks inverse gabungan ($M^{-1} = S^{-1} \cdot T^{-1}$) berdimensi $4 \times 4$ untuk mentransformasikan koordinat ray dunia (*World Space*) mundur kembali ke ruang lokal objek (*Local Space*) agar kalkulasi rumus tabrakan menjadi valid dan presisi.
3. **Quadratic Discriminant Analyzer:** Menghitung koefisien persamaan kuadrat kuadratik ($A, B, C$) berdasarkan parameter ray lokal untuk mendapatkan nilai Diskriminan ($D$). Aplikasi secara cerdas mendeteksi status tabrakan (Sinar Menembus, Menyerempet/Singgung, atau Luput) dan mengeluarkan nilai parameter jarak hit intersek ($t_1, t_2$) secara otomatis.

---

## 📜 History Prompting & Pengembangan Bersama AI Operative (Gemini)
Proses pengerjaan proyek-proyek ini dilakukan menggunakan metode *Vibe Coding* yang terstruktur bersama AI partner melalui beberapa fase iterasi berikut:

### 🔹 Fase 1: Inisialisasi Blueprints & Logika Matematika (Soal 1)
* **Prompt:** Menyerahkan foto lembar soal UAS halaman 1 dan meminta pembuatan struktur aplikasi web single-file menggunakan Tailwind CSS, Three.js, dan KaTeX untuk menangani perhitungan koordinat centroid $P$, cross product normal vector $\vec{N}$ dari dua vektor sisi segitiga, dan dot product $(\vec{N} \cdot \vec{L})$ untuk mendapatkan $\cos(\theta)$.
* **Solusi AI:** AI menyusun kerangka matematis murni menggunakan algoritma standard JavaScript `Math` object untuk memastikan kepatuhan 100% terhadap aturan larangan Generative AI runtime.

### 🔹 Fase 2: Resolusi Kendala Sinkronisasi Dependency & OrbitControls
* **Masalah Terdeteksi:** File OrbitControls eksternal dari CDN mengalami kegagalan *load* sinkronisasi yang menyebabkan kanvas 3D tidak muncul (stuck/blank viewport).
* **Solusi AI:** AI membuang script library OrbitControls tambahan dan mengimplementasikan fungsi kalkulasi rotasi kamera *custom trackball* (menggunakan formula spherical coordinates trigonometri murni lewat event listener mouse `mousedown`/`mousemove` bawaan vanilla JS). Hasilnya aplikasi menjadi 100% *self-contained* dan anti-gagal.

### 🔹 Fase 3: Pemisahan Modul Arsitektur Sistem Kamera (Soal 2)
* **Prompt:** Menginisialisasi pembuatan aplikasi terpisah untuk menangani parameter matriks optik kamera perspektif sesuai dengan instruksi Soal nomor 2, dengan batasan deployment harus terintegrasi langsung di dalam satu domain GitHub Pages yang sama.
* **Solusi AI:** AI memetakan seluruh kalkulasi aljabar linear penentu arah pandangan kamera untuk menyusun komponen baris-kolom matriks $4 \times 4$ ke dalam file mandiri `camera.html` agar rute panggilannya bersih dan teratur tanpa merusak dependensi Soal 1.

### 🔹 Fase 4: Implementasi Transformasi Terbalik / Inverse Space (Soal 3)
* **Prompt:** Mengembangkan modul aplikasi ketiga (`raytrace.html`) untuk menyelesaikan deteksi tabrakan sinar ray-object intersection. Sesuai batasan lembar soal halaman 2, perubahan ukuran (scale) dan posisi objek wajib dijabarkan menggunakan perkalian matriks transformasi inverse ($M^{-1}$).
* **Solusi AI:** AI mengintegrasikan rumus pemetaan koordinat ray terbalik, menyusun fungsi pencarian diskriminan kuadratik murni lewat vanilla JS, dan menampilkan trace perhitungannya secara real-time berdampingan dengan viewport interaktif.

---

## 📐 Alur Perhitungan Matematika Klasik yang Diterapkan
Aplikasi mengeksekusi fungsi kalkulasi internal murni di sisi klien dengan urutan:
* **Soal 1:** $P_{xyz} = \frac{A_{xyz} + C_{xyz} + E_{xyz}}{3} \rightarrow \vec{N}_{raw} = \vec{AC} \times \vec{AE} \rightarrow I = I_L \cdot K_d \cdot \max(0, \vec{N} \cdot \vec{L})$
* **Soal 2:** $\vec{n} = \frac{E - T}{|E - T|}, \vec{u} = \frac{\vec{Up} \times \vec{n}}{|\vec{Up} \times \vec{n}|}, \vec{v} = \vec{n} \times \vec{u} \rightarrow M_{view} \text{ dan } M_{proj} \text{ (Faktor fokus } f = \cot(\frac{FOV}{2}))$.
* **Soal 3:** $Ro_{local} = M^{-1} \cdot Ro_{world}, \ Rd_{local} = M^{-1}_{rot,scale} \cdot Rd_{world} \rightarrow D = B^2 - 4AC \rightarrow t = \frac{-B \pm \sqrt{D}}{2A}$
