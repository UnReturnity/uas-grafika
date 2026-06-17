soal 1: # 📑 Dokumentasi & History Prompting - UAS Grafika Komputer

## 👤 Informasi Mahasiswa
* **Nama:** Raymond Indrawan Wijaya
* **Program Studi:** S1 Informatika
* **Asal Institusi:** STTS Surabaya
* **Mata Kuliah:** Grafika Komputer (Genap 2025/2026)
* **Tanggal Pengerjaan:** 17 Juni 2026

---

## 🛠️ Deskripsi Aplikasi (Soal 1: Lambertian Diffuse Reflection)
Aplikasi ini merupakan visualizer interaktif berbasis web yang mensimulasikan pencahayaan klasik **Lambertian Diffuse Reflection** pada permukaan segitiga 3D dinamis tanpa menggunakan komponen Generative AI pada runtime aplikasi hasil akhir. 

### Fitur Utama:
1. **Interactive 3D Viewport:** Menggunakan library `Three.js` klasik untuk me-render bidang segitiga koordinat input secara *real-time* lengkap dengan indikator vektor normal ($\vec{N}$) warna biru dan vektor arah cahaya ($\vec{L}$) warna kuning.
2. **Dynamic Vertex Control:** Pengguna dapat mengubah koordinat kartesian ($X, Y, Z$) untuk ketiga sudut segitiga ($A, C, E$) secara manual untuk merubah bentuk geometri secara instan.
3. **Dynamic Lighting Control:** Slider interaktif untuk memanipulasi posisi sumber lampu virtual ($P_L$) dan nilai koefisien absorbsi warna material ($K_d$).
4. **Automated KaTeX Step-by-Step:** Menampilkan seluruh urutan kalkulasi linear matematika secara transparan seolah ditulis manual di atas kertas menggunakan formatting `KaTeX`. Setiap kali slider atau input diubah, angka di dalam langkah rumus ikut berhitung otomatis secara dinamis.

---

## 📜 History Prompting & Pengembangan Bersama AI Operative (Gemini)
Proses pengerjaan aplikasi ini dilakukan menggunakan metode *Vibe Coding* yang terstruktur bersama AI partner melalui beberapa fase iterasi berikut:

### 🔹 Fase 1: Inisialisasi Blueprints & Logika Matematika
* **Prompt Awal:** Menyerahkan foto lembar soal UAS halaman 1 dan meminta pembuatan struktur aplikasi web single-file menggunakan Tailwind CSS, Three.js, dan KaTeX untuk menangani perhitungan koordinat centroid $P$, cross product normal vector $\vec{N}$ dari dua vektor sisi segitiga, dan dot product $(\vec{N} \cdot \vec{L})$ untuk mendapatkan $\cos(\theta)$.
* **Hasil:** AI menyusun kerangka matematis murni menggunakan algoritma standard JavaScript `Math` object untuk memastikan kepatuhan 100% terhadap aturan larangan Generative AI runtime.

### 🔹 Fase 2: Resolusi Kendala Sinkronisasi Dependency (Debugging)
* **Masalah Terdeteksi:** File OrbitControls eksternal dari CDN mengalami kegagalan *load* sinkronisasi yang menyebabkan kanvas 3D tidak muncul (stuck/blank viewport).
* **Prompt Perbaikan:** Meminta AI mendiagnosis dan memberikan alternatif kode yang bebas dari error dependency eksternal.
* **Solusi AI:** AI membuang script library OrbitControls tambahan dan mengimplementasikan fungsi kalkulasi rotasi kamera *custom trackball* (menggunakan formula spherical coordinates trigonometri murni lewat event listener mouse `mousedown`/`mousemove` bawaan vanilla JS). Hasilnya aplikasi menjadi 100% *self-contained* dan anti-gagal.

### 🔹 Fase 3: Penyelarasan Fleksibilitas Parameter Soal
* **Masalah Terdeteksi:** Koordinat awal terkunci secara statis pada contoh Gambar 1 ($A(8,0,0), C(0,3,0), E(4,4,8)$), padahal instruksi soal meminta aplikasi bertindak sebagai media latihan umum di mana pengguna bisa memasukkan koordinat bidang acak secara manual.
* **Prompt Perbaikan:** Meminta penambahan input numerik dinamis agar bentuk segitiga bisa ikut berubah (warping/scaling) secara interaktif.
* **Solusi AI:** Mengintegrasikan 9 input box baru untuk memetakan koordinat dinamis sudut segitiga, melengkapi fungsi pembangunan ulang buffer geometri Three.js (`computeVertexNormals()`), dan menghubungkannya agar seluruh angka pecahan di dalam panel KaTeX ikut bergeser secara dinamis.

---

## 📐 Alur Perhitungan Matematika Klasik yang Diterapkan
Aplikasi mengeksekusi fungsi kalkulasi internal murni di sisi klien dengan urutan:
1. **Centroid Segitiga ($P$):** $P_{xyz} = \frac{VertexA_{xyz} + VertexC_{xyz} + VertexE_{xyz}}{3}$
2. **Vektor Sisi & Cross Product Normal ($\vec{N}_{raw}$):** $\vec{AC} = C - A$, $\vec{AE} = E - A \rightarrow \vec{N}_{raw} = \vec{AC} \times \vec{AE}$ lewat perhitungan determinan matriks $3 \times 3$.
3. **Normalisasi Vektor:** $\vec{N} = \frac{\vec{N}_{raw}}{|\vec{N}_{raw}|}$ dan $\vec{L} = \frac{P_L - P}{|P_L - P|}$
4. **Hukum Kosinus Lambert:** Intensitas Akhir Warna $I = I_L \cdot K_d \cdot \max(0, \vec{N} \cdot \vec{L})$
