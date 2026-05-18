# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---
---
## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap


EXPERIMENT DESIGN

"Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah?"
 
Hypothesis:
- H0: MAPE_Contextual-LSTM >= MAPE_Vanilla-LSTM (Tidak ada penurunan error yang signifikan)
- H1: MAPE_Contextual-LSTM < MAPE_Vanilla-LSTM (Integrasi fitur kontekstual menurunkan nilai error secara signifikan)
Latihan 1 - Desain Eksperimen
 
Tipe Eksperimen: Comparison & Ablation
 
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Menguji arsitektur LSTM standar sebagai baseline pembanding riset. | Vanilla LSTM (Tanpa data promo/libur). | Dataset Penjualan Ritel XYZ, Learning Rate 0.001, Optimizer Adam, Batch Size 32. |
| Treatment 1 | Menguji pengaruh parsial dari variabel promo internal saja (Ablation). | LSTM + Fitur Promo saja. | Dataset Penjualan Ritel XYZ, Learning Rate 0.001, Optimizer Adam, Batch Size 32. |
| Treatment 2 | Menguji pengaruh gabungan penuh dari seluruh fitur kontekstual (Full Usulan). | LSTM + Fitur Promo + Fitur Hari Libur Nasional. | Dataset Penjualan Ritel XYZ, Learning Rate 0.001, Optimizer Adam, Batch Size 32. |
 
 
Latihan 2 - Fairness Checklist
 
| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | Fair | Semua skema (Control dan Treatment) menggunakan basis berkas log transaksi dari toko retail fisik yang sama tanpa modifikasi record. |
| Preprocessing setara | Fair | Teknik penanganan missing value dan normalisasi data (MinMax Scaler) dilakukan serentak lewat satu pipeline induk yang sama. |
| Tuning effort setara | Fair | Jumlah lapisan tersembunyi (hidden layers), parameter dropout rate, dan batasan jumlah epochs dikunci sama besar di file konfigurasi. |
| Environment identik | Fair | Seluruh pengujian dijalankan pada mesin server lokal yang sama (spesifikasi CPU/GPU dan versi library TensorFlow yang identik). |
| Metrik evaluasi sama | Fair | Menggunakan blok kode matematika fungsi evaluasi yang sama untuk menghitung skor MAPE dan RMSE akhir. |
 
Ada yang tidak fair? Tidak
 
Justifikasi: Tidak ada ketidakadilan pengujian, karena arsitektur jaringan Deep Learning ditahan konstan (CV) dan satu-satunya hal yang diubah (swap/toggle) hanyalah dimensi jumlah kolom matriks input data yang diumpankan ke model (IV).
 
 
Latihan 3 - Threat Analysis
 
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Perubahan drastis layout fisik tata letak barang di toko selama masa pencatatan data yang mengubah psikologi belanja konsumen. | Mengonfirmasi kepada pihak manajemen ritel untuk memastikan data diambil pada periode operasional yang stabil tanpa perombakan ekstrim toko. |
| External | Pola belanja musiman masyarakat sangat terikat dengan budaya lokal (misal: lonjakan THR Lebaran di Indonesia), sehingga model tidak akurat jika dibawa ke luar negeri. | Menjelaskan secara eksplisit di bab batasan penelitian bahwa konteks makro riset ini adalah karakteristik pasar ritel domestik Indonesia. |
| Construct | Nilai MAPE bisa menghasilkan angka tidak terdefinisi (infinity) apabila angka penjualan riil menyentuh 0 unit. | Menggunakan formula alternatif Symmetric MAPE (sMAPE) atau MASE (Mean Absolute Scaled Error) sebagai pengaman pendukung. |
| Conclusion | Ukuran sampel data transaksi terlalu pendek (misal hanya 3 bulan), sehingga model gagal membuktikan pola musiman tahunan secara valid. | Mewajibkan batas minimal panjang data historis yang ditarik dari sistem POS minimal selama 2 hingga 3 tahun kalender penuh. |
 
Ancaman paling sulit dimitigasi: External Validity (Konteks Musiman Lokal)
 
Karena perilaku konsumen ritel kelas menengah di Indonesia sangat dipengaruhi oleh budaya unik (seperti fenomena mudik dan pencairan dana THR menjelang Idulfitri) yang polanya tidak ditemukan pada dataset ritel global populer seperti Walmart (AS). Oleh karena itu, generalisasi model ini akan selalu terbatas pada wilayah dengan budaya demografis sejenis.
 
 
Refleksi
 
Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Berikut 3 pertanyaan evaluasi kritis:
 
1. Apakah baseline sudah di-tuning dengan usaha yang setara (fair tuning effort)?
   Atau baseline sengaja dibiarkan menggunakan default parameters agar terlihat lemah? (Mengecek adanya Straw Man Comparison)
2. Apakah pembagian dataset menggunakan kaidah yang benar (Time-Series Split)?
   Atau terjadi kebocoran data (Data Leakage) yang membuat metode usulan terlihat unggul secara semu? (Mengecek Internal Validity)
3. Apakah perbaikan metrik sudah diuji secara signifikansi statistik (P-Value < 0.05)?
   Atau selisih keunggulannya sangat tipis dan masuk dalam rentang margin error acak? (Mengecek Conclusion Validity)
---
