# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Model peramalan stok berbasis LSTM saat ini sering mengalami penurunan akurasi yang signifikan pada periode puncak (peak season) karena tidak mengintegrasikan variabel kontekstual eksternal seperti data promo dan hari libur nasional.____________________

Research Question:
  Tipe         :  [ ] Improvement  
  Formulasi    : _Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah_________________
  Variabel IV  : Integrasi fitur kontekstual____________________
  Variabel DV  : Akurasi peramalan (Error Rate).____________________
  Metrik       : MAPE (Mean Absolute Percentage Error) dan RMSE (Root Mean Square Error).____________________
  Dataset      :Data transaksi historis ritel (Januari 2023 - Desember 2025).___________________
  Baseline     : Vanilla LSTM (Tanpa fitur kontekstual)____________________

Quality Check RQ:
  [x ] Variabel spesifik
  [x ] Metrik jelas
  [ x] Baseline ada
  [ x] Konteks disebutkan
  [ x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui :Pengaruh signifikansi penyertaan data eksternal terhadap stabilitas model prediksi stok pada kondisi fluktuatif. ____________________
  Jenis kontribusi        : [x ] Improvement  
  Gap yang diisi          : Mengatasi kelemahan model LSTM standar dalam menangani outlier musiman pada manajemen stok.____________________

Hypothesis Pair:
H₀: Tidak ada penurunan nilai MAPE yang signifikan ($\le 5\%$) antara model LSTM dengan fitur kontekstual dibandingkan dengan Vanilla LSTM.
H₁: Integrasi fitur kontekstual pada model LSTM memberikan penurunan nilai MAPE yang signifikan ($> 5\%$) dibandingkan dengan Vanilla LSTM.
Threshold: Penurunan MAPE sebesar 5%.
Justifikasi threshold: Berdasarkan literatur (Abbasimehr, 2020), perbaikan akurasi di atas 5% pada industri ritel sudah memberikan dampak efisiensi biaya penyimpanan yang besar. 

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Model peramalan stok gagal menangkap lonjakan permintaan saat event promo karena hanya mengandalkan data histori penjualan tunggal.____________________________________

**RQ versi pertama (tulis bebas):**
> Bagaimana cara membuat LSTM jadi lebih akurat buat prediksi stok kalau lagi ada promo?___________________________________________________

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
|Metode spesifik|Ya|LSTM dengan fitur kontekstual|
|Metrik terukur|Ya|MAPE / RMSE|
|Baseline|Ya|Vanilla LSTM|
|Dataset/konteks|Ya|Dataset ritel menengah|

**Tipe RQ:* [ ] Improvement 

**RQ versi revisi (setelah evaluasi):**
> Sejauh mana penambahan fitur promo dan hari libur sebagai input variabel pada model LSTM dapat meningkatkan akurasi prediksi stok (menurunkan RMSE) dibandingkan dengan model LSTM standar pada periode high-demand___________________________________________________

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
|H₀|Model LSTM dengan fitur tambahan tidak memberikan akurasi yang lebih baik daripada model standar|
|H₁|Model LSTM yang diintegrasikan dengan fitur promo memiliki nilai RMSE yang lebih rendah secara signifikan dibandingkan model standar|
|Metrik|Root Mean Square Error (RMSE)|
|Threshold|P-Value < 0.05 (Signifikansi statistik) atau reduksi RMSE > 10%|
|Justifikasi threshold|"Standar deviasi pada data ritel biasanya besar, sehingga perubahan 10% dianggap sebagai perbaikan yang substansial|

**Apakah hipotesis ini falsifiable?** [ ] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika setelah eksperimen dilakukan, nilai RMSE model baru justru lebih tinggi atau sama dengan model lama, maka H₁ ditolak dan riset membuktikan bahwa fitur tambahan tidak berpengaruh. ___________________

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
|RQ|Apakah LSTM + Fitur Kontekstual lebih akurat dari Vanilla LSTM|
|Variable (IV)|Arsitektur model (LSTM Standar vs LSTM Kontekstual)|
|Variable (DV)|Error Prediksi (MAPE).|
|Metric|Persentase kesalahan rata-rata ($MAPE = \frac{1}{n} \sum|
| data source|Log penjualan dan tabel promosi internal perusahaan|
|Analysis method|Comparative Performance Analysis (Uji-T atau Wilcoxon signed-rank test)|

**Apakah rantai lengkap?** [ ] Ya 
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Sales Forecasting using LSTM Network: A Case Study in Retail Industry (Abbasimehr et al., 2020).Sales Forecasting using LSTM Network: A Case Study in Retail Industry (Abbasimehr et al., 2020)._____________________________________________
**RQ yang diekstrak:** Dapatkah model LSTM menghasilkan prediksi yang lebih baik dibandingkan dengan metode ARIMA dan ANN?__________________________________
**Komponen yang hilang:** RQ tersebut sudah cukup baik, namun kurang spesifik pada dataset yang digunakan dalam kalimat pertanyaannya. RQ yang ideal seharusnya mencantumkan batasan dataset (misal: "pada data penjualan furnitur") agar ruang lingkup riset tidak melebar ke industri lain yang karakteristik datanya berbeda._______________________________
