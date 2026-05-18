# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah____________________

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Arsitektur Model|IV|Pendekatan pemodelan sekuensial deret waktu|Jenis konfigurasi input model (Vanilla LSTM vs Contextual-LSTM)|Nominal|-|Menentukan variasi perlakuan algoritma pada eksperimen|Pembanding langsung untuk melihat efek intervensi fitur tambahan|
|Akurasi Peramalan|DV|Tingkat kedekatan hasil prediksi stok terhadap permintaan aktual|Mean Absolute Percentage Error (MAPE)|Ratio|Persen (%)|Menghitung rata-rata persentase absolut selisih prediksi dengan nilai riil|Standardisasi internasional untuk mengukur performa model forecasting ritel|
|Karakteristik Data Historis|CV|Konsistensi data masa lalu yang digunakan untuk training|Rentang waktu pengerjaan data (Sliding Window 12 bulan)|Ratio|Bulan|Membatasi panjang memori deret waktu yang dipelajari model|Menjamin kestabilan lingkungan pengujian agar adil (fair comparison)|

Alignment Check:
   RQ (Apakah Contextual-LSTM menurunkan error?) $\rightarrow$ Concept (Akurasi Prediksi Stok) $\rightarrow$ Variable (DV: Performa Model) $\rightarrow$ Metric (MAPE) $\rightarrow$ Data (Hasil hitung deviasi) $\rightarrow$
 Result (Persentase penurunan error).
[X]Setiap langkah terdokumentasi
[X]Tidak ada "lompatan logis"
[X] Metrik mengukur apa yang dimaksud (construct validity)
---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** _Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah?"_________________________________________________

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
|Arsitektur Model|IV|Metode pemrosesan data deret waktu ritel| Kategori input (0: Tanpa Fitur, 1: Dengan Fitur Eksternal)|Nominal|
|Kesalahan Prediksi|DV|Tingkat penyimpangan kuantitatif model|Nilai MAPE dan RMSE hasil pengujian test-set|Ratio|Persen (%) & Unit Produk|
|Periode Waktu Data|CV|Durasi siklus operasional bisnis|Batasan temporal data historis (3 tahun kalender transaksi)|Ratio|Tahun|
**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? Rantai penelusuran sangat linier. Konsep abstrak mengenai "akurasi/kesalahan prediksi" langsung diterjemahkan ke dalam formula matematika MAPE yang menghitung selisih unit barang secara absolut terhadap angka riil penjualan.____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
|Representative|5|MAPE mewakili persentase kesalahan yang intuitif bagi manajer gudang dalam mengukur penyimpangan stok|
|Sensitive|4|"Cukup peka terhadap fluktuasi perubahan kecil per hari, namun rentan terganggu jika ada nilai penjualan aktual yang bernilai nol (0)."|
|Feasible|5|Sangat mudah dihitung menggunakan pustaka komputasi standar (Scikit-Learn / TensorFlow dalam Python)|.
**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? _Perlu menyertakan RMSE (Root Mean Square Error) sebagai metrik sekunder. Karena MAPE mengukur persentase kesalahan rata-rata secara merata, sedangkan RMSE memberikan penalti bobot yang lebih tinggi pada kesalahan prediksi berskala besar (lonjakan ekstrim), yang sangat krusial dalam mendeteksi risiko stockout parah.____________________________

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika model diuji pada barang yang sangat jarang laku (extremely slow-moving items) di mana penjualannya hampir selalu bernilai 0 atau 1 unit per hari, perubahan performa algoritma yang canggih tidak akan terlihat signifikan pada nilai MAPE karena efek pembagi nol atau fluktuasi persentase yang terdistorsi secara ekstrim.___________________________________________________

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
|Completeness|Apakah semua data point terkumpul|Berpotensi ada hari di mana toko tutup atau sistem POS error sehingga terjadi missing value|Menerapkan metode Imputation (seperti Linear Interpolation atau pengisian nilai 0 pada tanggal libur resmi toko)|
|Consistency|Apakah ada kontradiksi internal|Ada kemungkinan pencatatan retur barang memotong total penjualan harian secara rancu|Melakukan data cleaning untuk memisahkan data penjualan kotor (gross sales) dengan penyesuaian retur terpisah|
|Validity|Apakah benar-benar mengukur yang dimaksud?|"Ya, jumlah barang keluar di kasir merepresentasikan permintaan riil pasar pada hari tersebut|",Memvalidasi silang (cross-check) total transaksi harian POS dengan data fisik pengurangan stok di gudang utama|
|Representativeness|Apakah sampel mewakili populasi target?|"Data 3 tahun terakhir mencakup siklus musiman tahunan penuh (Ramadan, akhir tahun) di Indonesia|",Memastikan pembagian data train dan test menjaga struktur urutan waktu (Time-Series Split) agar pola musiman terwakili adil|
## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
 Memilih metrik setelah melihat hasil data eksperimen dianggap sebagai p-hacking (atau data-dredging) karena tindakan tersebut merusak objektivitas ilmiah. Ketika peneliti melihat data terlebih dahulu, mereka cenderung secara sadar atau tidak sadar memilih metrik tertentu yang hanya memenangkan hipotesis mereka (membuat nilai p-value tampak signifikan), sementara mengabaikan metrik lain yang menunjukkan kegagalan model.

Perbedaannya dengan eksplorasi data yang sah (Exploratory Data Analysis) adalah pada tujuannya. Eksplorasi data dilakukan di awal riset sebelum algoritma diuji, dengan tujuan memahami karakteristik dasar data (mencari pola, distribusi, dan tren). Hasil eksplorasi digunakan untuk merumuskan hipotesis dan menetapkan metrik secara transparan by design, bukan memanipulasi parameter keberhasilan di akhir eksperimen demi membuat laporan terlihat "bersih".__________________________________________________
> ___________________________________________________
