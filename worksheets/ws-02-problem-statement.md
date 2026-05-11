# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : ___Supply Chain Management & Predictive Analytics._________________
  Konteks  : _Manajemen stok barang pada toko ritel menengah yang memiliki fluktuasi permintaan tinggi.___________________

System Context
  Input       : Data transaksi penjualan historis (bulanan/harian), data kategori barang, dan kalender hari libur/promo.____________________
  Process     : Analisis data deret waktu (time-series) dan pengenalan pola musiman menggunakan algoritma LSTM (Long Short-Term Memory).____________________
  Output      : Estimasi jumlah stok yang harus dipesan (Reorder Point) untuk periode mendatang.____________________
  Outcome     : Pengurangan biaya operasional (biaya simpan) dan penghindaran stockout (stok kosong).____________________
  Constraints : Anggaran pengadaan terbatas dan kapasitas gudang yang tidak fleksibel.____________________
  Stakeholders: Manajer Logistik, Bagian Keuangan, dan Tim IT Operasional.____________________

Fenomena → Problem
  Fenomena yang diamati             : terjadi ketidakseimbangan stok yang parah (barang laku sering kosong, barang lambat menumpuk).____________________
  Gejala (symptom) yang terukur     :Angka Lost Sales Opportunity sebesar 18% dan nilai kerugian akibat barang kadaluarsa/rusak di gudang meningkat 12%. ____________________
  Masalah yang didiagnosis          : Sistem manajemen stok yang ada masih bersifat reaktif (hanya pesan jika habis) dan tidak mampu memprediksi lonjakan permintaan di masa depan.____________________
  Masalah riset (researchable)      : Sejauh mana model Deep Learning LSTM dapat memprediksi fluktuasi permintaan secara akurat pada data penjualan yang memiliki variansi tinggi?____________________
  Variabel yang terukur             : Mean Absolute Percentage Error (MAPE) dan Root Mean Square Error (RMSE).____________________

Problem Quality Check
  [x] Clarity — Fokus pada inakurasi prediksi jumlah stok.
  [x] Measurability — Kesalahan prediksi diukur dengan metrik MAPE/RMSE.

  [x] Relevance — Berkontribusi langsung pada efisiensi modal kerja perusahaan.

  [x] Testability — Dapat diuji dengan membandingkan prediksi model vs kenyataan penjualan.

  [x] Impact — Mampu menyelamatkan potensi kerugian finansial akibat inefisiensi stok.

Problem Statement (1 paragraf):
  __Toko ritel menghadapi kendala manajemen inventaris di mana penggunaan metode prediksi manual mengakibatkan tingginya angka lost sales sebesar 15% akibat stok habis dan penumpukan deadstock sebesar 20%. Masalah ini disebabkan oleh ketidakmampuan metode konvensional dalam menganalisis pola permintaan konsumen yang bersifat non-linear dan musiman. Penelitian ini bertujuan untuk mengimplementasikan algoritma LSTM guna menghasilkan prediksi kebutuhan stok yang lebih akurat, sehingga perusahaan dapat mengoptimalkan biaya operasional dan meningkatkan ketersediaan barang secara tepat waktu.__________________
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** __Manajemen stok otomatis______________________________________

| Tahap | Hasil |
|-------|-------|
| Reality | Banyak barang di gudang yang berdebu karena tidak laku, sementara rak di toko kosong.* |
| Observed Issue (Symptom) | Biaya penyimpanan meningkat dan pelanggan mengeluh barang sering kosong.|
| Diagnosed Problem (Root Cause) |Metode Moving Average yang digunakan saat ini terlalu sederhana untuk menangkap tren musiman. |
| Researchable Problem |Perbandingan akurasi antara metode statistik tradisional vs LSTM dalam konteks Inventory Forecasting. |
| Measurable Variable |Nilai MAPE (tingkat kesalahan persentase) dalam hasil peramalan. |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x ] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | *Data penjualan 3 tahun terakhir dan kalender promosi.* |
| Process |Pelatihan model untuk mengenali pola musiman (misal: kenaikan stok saat Lebaran/Natal). |
| Output |Daftar jumlah pesanan barang yang disarankan. |
| Outcome |Ketersediaan stok naik menjadi 95% dengan biaya gudang turun 10%. |
| Constraints |Kecepatan server untuk memproses data besar (Big Data). |
| Stakeholders |Admin gudang yang memerlukan panduan belanja barang. |

**Komponen mana yang paling relevan dengan masalah riset?** _Output.
Karena output berupa angka prediksi yang akurat adalah solusi kunci untuk menyelesaikan masalah penumpukan stok.______________

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5	 | Masalah sangat spesifik pada akurasi prediksi.* | |
| Measurability |5 |Menggunakan standar error statistik yang jelas |
| Relevance |5 | Sangat dibutuhkan oleh industri ritel manapun.|
| Testability |5 |Hipotesis "LSTM lebih baik dari rata-rata" sangat mudah diuji. |
| Impact | 5|Berdampak langsung pada keuntungan bersih perusahaan. |

**Skor total:** ___25__ / 25

**Problem statement versi final (1 paragraf):**
> __Manajemen inventaris pada gudang ritel saat ini masih menghadapi masalah inefisiensi yang ditandai dengan tingginya angka lost sales sebesar 18% akibat ketidakakuratan prediksi permintaan. Hal ini disebabkan oleh keterbatasan sistem konvensional dalam menganalisis pola perilaku konsumen yang dinamis dan terikat waktu. Penelitian ini bertujuan untuk mengimplementasikan algoritma LSTM guna membangun sistem manajemen stok otomatis yang mampu meramalkan kebutuhan barang secara presisi, sehingga meminimalkan biaya penyimpanan sekaligus menjaga ketersediaan stok di level optimal.____________________________________
> ___________________________________________________

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan fundamentalnya adalah pada Logika Investigasi. Masalah coding (bug) diselesaikan dengan melacak alur eksekusi program untuk menemukan baris kode yang rusak (How to fix). Namun, masalah riset diselesaikan dengan membangun argumen berbasis data untuk mengisi kekosongan pengetahuan (Why it happens). Dalam manajemen stok, "bug" mungkin adalah sistem tidak mau memunculkan angka, tapi "masalah riset" adalah angka yang muncul tidak akurat dan kita harus membuktikan metode mana yang paling mendekati kenyataan.___________________________________________________
> ___________________________________________________
