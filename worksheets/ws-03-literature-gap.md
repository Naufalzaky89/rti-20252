# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : _Manajemen Stok Otomatis menggunakan Deep Learning (LSTM)___________________
Database   : _Google Scholar, ResearchGate, IEEE Xplore___________________
Query      : ("inventory forecasting" OR "demand prediction") AND ("LSTM" OR "Deep Learning") AND "Retail"____________________
Tahun      : 20221-2025____________________
Hasil awal : _38___ paper → Screening → __5__ paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Abbasimehr et al.|2020|Multi-layer LSTM|Furniture Sales|MAPE 8.2%|Hanya menggunakan data internal histori penjualan tunggal|
Kanwal et al|2022|Bi-LSTM + GRU|Grocery Store|Acc 94%|Arsitektur terlalu kompleks untuk perangkat komputasi rendah|
Bansal et al|2023|Hybrid ARIMA-LSTM|FMCG Data|RMSE 12.4|Gagal memprediksi lonjakan mendadak akibat event promo|
Gao et al|2024|Attention-LSTM|E-commerce|MAE rendah|"Fokus hanya pada barang Fast-Moving, mengabaikan Slow-Moving."|
Putra et al|2024|LSTM + XGBoost|Retail Lokal|MAPE 11.5%|Dataset sangat terbatas pada satu kategori barang saja|     

Pola yang ditemukan:
  Metode dominan     : Penggunaan varian LSTM (Bi-LSTM atau Hybrid) untuk menangkap pola time-series.____________________
  Dataset umum       :Dataset kompetisi M5 atau data ritel besar (E-commerce). ____________________
  Limitasi berulang  : model kesulitan menangkap fluktuasi stok akibat variabel eksternal (hari libur, cuaca, atau promo kompetitor).____________________

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : Kurangnya penelitian yang menguji ketangguhan LSTM pada ritel skala menengah dengan fluktuasi harga yang ekstrim.____________________
  Bukti        : Sebagian besar literatur (Abbasimehr, Gao) menggunakan dataset yang sudah teratur dan stabil.____________________
  Signifikansi : Ritel menengah seringkali memiliki pola yang lebih "berisik" (noisy), sehingga butuh model yang lebih adaptif.____________________

Gap 2: [Jenis:method gap]
  Deskripsi    : _Belum banyak integrasi data eksternal (promo lokal & hari raya) sebagai fitur pendukung pada arsitektur LSTM.___________________
  Bukti        : Bansal et al. (2023) mengakui kelemahan modelnya saat terjadi lonjakan pesanan mendadak di luar histori rutin.____________________
  Signifikansi : Menambahkan fitur kontekstual dapat menurunkan angka lost sales secara signifikan____________________

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|ARIMa|Metode statistik standar untuk peramalan|Digunakan sebagai pembanding utama di 80% literatur|Bansal et al., 2023|
|Vanilla LSTM|Model dasar Deep Learning untuk sekuensial|Merupakan standar emas riset saat ini|"Abbasimehr et al., 2020"|        
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Optimasi Prediksi Stok Ritel menggunakan Integrasi LSTM dan Variabel Kontekstual.****________________________________________
**Query pencarian:** _("LSTM") AND ("Inventory forecasting") AND ("Contextual features")___________________________________
**Database:** Google Scholar & ResearchGate.___________________________________________

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 |Abbasimehr|	2020|	Multi-layer LSTM|	Retail sales|	MAPE 8%|	Tidak ada data promo|
| 2 |Kanwal|	2022|	Bi-LSTM|	Supermarket|	Acc 94%|	Komputasi berat|
| 3 | Bansal|	2023|	ARIMA-LSTM|	FMCG|	RMSE 12.4|	Gagal saat event mendadak|
| 4 | Gao|	2024|	Attention-LSTM|	Walmart Data|	MAE 0.05|	Hanya barang laku|
| 5 | Putra|	2024|	Hybrid ML|	Lokal UKM|	MAPE 11%|Data homogen|

**Pola yang terlihat — Metode dominan:** dipilih karena kemampuannya dalam Long-term dependencies (mengingat tren masa lalu yang jauh).___________________
**Limitasi yang berulang:** Model bersifat tertutup (hanya melihat histori angka sendiri) tanpa melihat konteks lingkungan (Hari Raya, Promo)______________________________

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
Performance Gap| Ya|Akurasi anjlok (MAPE > 20%) saat terjadi outlier musim liburan|
Method Gap| Ya|Belum ada penggunaan Attention Mechanism untuk pembobotan fitur promo|
Data Gap| Tidak|Data historis penjualan tersedia cukup melimpah|
Context Gap| Ya|Model belum diuji pada dinamika pasar ritel di Indonesia|

**Gap utama yang dipilih:** ntegrasi fitur kontekstual (promo & hari libur) pada model LSTM untuk meningkatkan akurasi peramalan stok pada periode puncak (peak season)._____________________________
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> _Karena kesalahan prediksi saat hari besar berakibat fatal secara finansial: stok habis berarti kehilangan pendapatan besar, stok berlebih berarti modal mati dalam jumlah besar.__________________________________________________

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
|1|ARIMA,Standar statistik|Paling banyak dipakai industri|Bukan|Bansal (2023)|
|2|Vanilla LSTM|Standar deep learning|Benchmark riset terbaru|Ya (Basic)|,Abbasimehr (2020)|


**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ] Tidak
> Justifikasi:Tidak, karena ARIMA adalah standar industri yang valid dan Vanilla LSTM adalah standar riset yang jujur. Saya tidak membandingkannya dengan metode "asal-asalan". ________________________________________

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> klaim "belum ada yang meneliti ini" biasanya bersifat subjektif dan sering kali salah jika literatur tidak dicari dengan teliti. Sebaliknya, Research Gap yang valid harus didukung oleh bukti tertulis dari literatur (seperti tabel matriks di atas) yang menunjukkan batasan konkret dari studi sebelumnya. Cara membuktikannya adalah melalui Literature Mapping; jika kita bisa memetakan 10 paper dan semuanya memiliki kelemahan yang sama, maka gap tersebut nyata dan terbukti ada.___________________________________________________
> ___________________________________________________
