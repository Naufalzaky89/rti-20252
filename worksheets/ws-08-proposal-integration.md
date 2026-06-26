# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [ ] Problem → Gap: masalah terdokumentasi di literatur
  [ ] Gap → RQ: pertanyaan menjawab gap spesifik
  [ ] RQ → Hypothesis: hipotesis memprediksi jawaban
  [ ] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [ ] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [ ] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [ ] Istilah sama di semua bagian
  [ ] Variabel di RQ = variabel di hipotesis = metrik di desain
  [ ] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [ ] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [ ] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [ ] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [ ] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [ ] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        |      |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   |      |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |      |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   |      |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Toko ritel menghadapi kendala manajemen inventaris dengan tingginya angka lost sales sebesar 18% akibat stok habis di saat puncak penjualan, dan penumpukan deadstock sebesar 20% yang menyebabkan kerugian finansial. Masalah ini disebabkan oleh ketidakmampuan sistem prediksi manual dalam menganalisis pola permintaan yang bersifat non-linear dan musiman. |
| Gap | WS-03 | Model peramalan stok berbasis LSTM saat ini mengalami penurunan akurasi signifikan pada periode puncak karena tidak mengintegrasikan variabel kontekstual eksternal seperti data promo dan hari libur nasional; literatur menunjukkan limitasi berulang dalam menangkap fluktuasi akibat faktor eksternal ini. |
| RQ | WS-04 | Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah? |
| Hipotesis | WS-04 | H₁: Integrasi fitur kontekstual pada model LSTM memberikan penurunan nilai MAPE yang signifikan (> 5%) dibandingkan dengan Vanilla LSTM; H₀: Tidak ada penurunan nilai MAPE yang signifikan (≤ 5%) antara kedua model. |
| Variabel & Metrik | WS-05 | IV = Arsitektur Model (Vanilla LSTM vs Contextual-LSTM); DV = Akurasi Peramalan diukur dengan MAPE (%) dan RMSE; CV = Periode Waktu Data (3 tahun kalender transaksi historis dengan sliding window 12 bulan). |
| Sistem | WS-06 | Sistem terdiri dari 3 modul modular: (1) Feature Engineering Pipeline untuk mengaktifkan/menonaktifkan fitur eksternal, (2) LSTM Model Engine dengan konfigurasi terkunci (learning rate 0.001, optimizer Adam, batch size 32), (3) Metrics Logger & Visualization Dashboard untuk otomatis menghitung MAPE dan RMSE. |
| Desain Eksperimen | WS-07 | Comparison & Ablation Study dengan 3 kondisi: (1) Control — Vanilla LSTM tanpa fitur eksternal, (2) Treatment 1 — LSTM + fitur promo saja, (3) Treatment 2 — LSTM + fitur promo + hari libur nasional; semua diuji pada dataset identik dengan preprocessing dan environment yang sama. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅ Kuat | Lost sales 18% dan deadstock 20% (Bab 2) muncul dari analisis 5 paper pada Bab 3 yang menunjukkan model LSTM tanpa fitur eksternal gagal menangkap fluktuasi musiman dan promo; gap jelas terdokumentasi dari literatur. |
| Gap → RQ | ✅ Kuat | RQ langsung menanyakan "apakah integrasi fitur kontekstual menurunkan MAPE?" — pertanyaan ini menjawab gap yang teridentifikasi tentang variabel eksternal yang belum diintegrasikan. |
| RQ → Hypothesis | ✅ Kuat | H₁ memprediksi penurunan MAPE > 5% sebagai hasil dari integrasi fitur kontekstual; threshold 5% dijustifikasi dari literatur Abbasimehr (2020) sebagai dampak efisiensi biaya penyimpanan yang material. |
| Hypothesis → Metric | ✅ Kuat | MAPE dan RMSE adalah metrik standar internasional untuk forecasting ritel yang secara langsung mengukur variabel dependent (akurasi peramalan) yang diprediksi dalam H₁. |
| Metric → System | ✅ Kuat | Metrics Logger & Visualization Dashboard (komponen sistem) otomatis menghitung MAPE dan RMSE dari output model; Hyperparameter Config Layer mengunci CV; Feature Engineering Pipeline memanipulasi IV — semua metrik bisa dihasilkan sistem. |
| System → Experiment | ✅ Kuat | Desain eksperimen (3 kondisi: Control, Treatment 1, Treatment 2) menggunakan sistem sebagai instrumen pengujian; setiap kondisi mensimulasi variasi IV (fitur eksternal) sambil menahan CV dan dataset tetap; hasil MAPE/RMSE dari sistem menjawab RQ. |

**Koneksi mana yang paling lemah?** Semua koneksi kuat; tidak ada koneksi yang lemah.

**Bagaimana cara memperkuatnya?** Tidak diperlukan penguatan; red thread proposal sudah koheren dari problem hingga eksperimen.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** ✅ Ya

> **Bukti konsistensi:**
> - "LSTM dengan integrasi fitur kontekstual" muncul konsisten di Problem  → Gap (WS-03) → RQ (WS-04) → Sistem (WS-06) → Eksperimen (WS-07).
> - Istilah "MAPE" dan "RMSE" digunakan sebagai metrik DV di semua bagian (WS-04, WS-05, WS-07).
> - Scope dataset tetap sama: "data transaksi ritel historis 3 tahun (Januari 2023 - Desember 2025)" dari problem hingga eksperimen.
> - Baseline "Vanilla LSTM" selalu dirujuk sebagai kontrol dalam perbandingan.

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Semua 6 koneksi vertikal terhubung dengan jelas — dari problem (lost sales 18%, deadstock 20%) → gap (model tanpa fitur eksternal) → RQ spesifik → hipotesis terukur → metrik konkret (MAPE, RMSE) → sistem modular → eksperimen fair dengan 3 kondisi. Red thread tidak ada yang putus. |
| Specificity | 3 | Semua variabel terdefinisi konkret: IV (Vanilla LSTM vs Contextual-LSTM), DV (MAPE dalam %, RMSE dalam unit produk), CV (data 3 tahun, learning rate 0.001, batch size 32, optimizer Adam). Threshold ditetapkan numerik (5% penurunan MAPE). Tidak ada abstraksi yang tidak jelas. |
| Feasibility | 3 | Timeline realistis 1-3 bulan: data historis sudah tersedia (2023-2025), framework LSTM matang, hyperparameter terbatas (tidak ada extensive tuning), ablation study 3 kondisi saja. Environment identik pada satu server lokal. Tidak ada ketergantungan eksternal yang kompleks. |
| Rigor | 3 | 2+ baseline dan SOTA dipilih dengan justifikasi: Vanilla LSTM sebagai baseline teknis (common practice 2020-2022), Contextual-LSTM sebagai novel approach yang mengintegrasikan fitur yang belum dikombinasikan di literatur. Ablation study (Treatment 1) menunjukkan kontribusi parsial fitur promo. Fairness checklist lengkap (dataset identik, preprocessing setara, tuning effort setara, environment identik, metrik sama). |

**Skor total:** 12 / 12

**Apakah proposal siap untuk fase eksekusi?** ✅ Ya

> **Alasan siap eksekusi:**
> 1. **Semua variabel sudah operasionalisasi** — Tidak ada konsep abstrak yang tertinggal; semua bisa diukur dan diimplementasikan.
> 2. **Sistem sudah dirancang modular** — Feature toggles (config YAML) memudahkan switch IV tanpa mengubah kode; variable isolation tercapai.
> 3. **Eksperimen sudah terspesifikasi** — 3 kondisi jelas, fairness terjamin, metrik pre-registered, tidak ada p-hacking risk.
> 4. **Literatur sudah di-map** — 5 paper foundational sudah dikompilasi; gap sudah diidentifikasi; positioning sudah jelas.
> 5. **Timeline realistis** — Tidak optimistik; sudah termasuk buffer 30-50% untuk debug dan validasi hasil.
> 
> **Catatan penting sebelum eksekusi:**
> - Pastikan data historis 2023-2025 sudah dibersihkan (missing values, outliers) sebelum eksperimen
> - Pre-register metrik ini di OSF (Open Science Framework) atau dokumentasi internal untuk menghindari p-hacking
> - Lakukan random seed locking di semua training untuk reprodusibilitas
> - Siapkan log eksperimen terstruktur (experiment ID, kondisi, timestamp, hasil) untuk traceability penuh

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** WS-05 (Variabel & Metrik) — karena literatur sudah jelas menunjukkan MAPE dan RMSE sebagai standar internasional untuk forecasting; operasionalisasi langsung tersedia dan tidak perlu kreativitas tinggi.

**Bagian tersulit:** WS-03 (Literature Mapping & Gap) — pencarian paper di database publik membutuhkan query Boolean yang presisi, snowballing manual makan waktu, dan gap yang ditemukan harus cukup "narrow" (tidak terlalu luas tapi juga tidak terlalu spesifik). Kesulitan lain adalah membedakan performance gap (metrik rendah) vs method gap (pendekatan belum ada) — keduanya valid tapi strategi mitigasi berbeda.

**Yang akan dilakukan berbeda:**

1. **Mulai dari problem yang lebih sharp** — Pada WS-02, saya butuh 2-3 minggu diskusi dengan domain expert (manajer logistik ritel) untuk memastikan problem statement bukan "general inefficiency" tapi spesifik ke "LSTM accuracy drop 15% saat peak season due to absence of external context variables". Problem yang sharp akan membuat gap search di WS-03 jauh lebih targeted.

2. **Operasionalisasi lebih awal** — Di WS-04, seharusnya sudah draft RQ dengan metrik spesifik (bukan "accuracy" tapi "MAPE > 5%") — ini akan menghindari backtrack saat WS-05 mencoba operasionalisasi konsep abstrak yang masih longgar.

3. **Integration loop lebih ketat** — Jangan tunggu sampai WS-08 untuk check koneksi vertikal. Setelah setiap WS baru, check 2-3 koneksi terdekat (misalnya selesai WS-04, langsung cek RQ → Hypothesis → Metric sebelum melanjutkan ke WS-05). Ini akan menangkap gap logic lebih dini.

4. **Sistem design lebih early** — WS-06 seharusnya di-draft lebih awal (setelah WS-05 selesai, bukan menunggu WS-07) untuk memastikan sistem feasible. Jika sistem tidak bisa measure DV spesifik, akan ketahuan sebelum terlambat — jangan sampai RQ → Metric → System ada gap di langkah ketiga.

5. **Fairness plan dibuat konkret** — Di WS-07, fairness checklist terasa abstrak. Seharusnya, fairness plan diwujudkan sebagai:
   - Checklist preprocessing code (sama untuk semua kondisi)
   - Mock config files untuk tiap kondisi (Control, Treatment 1, Treatment 2) — jadi tidak ada ambiguitas saat eksekusi
   - Screenshot environment setup (versi library, spesifikasi server) — save sebagai baseline untuk audit trail

Dengan perubahan ini, proses WS-01 sampai WS-08 akan lebih **feedforward** (tidak perlu banyak backtrack) dan lebih **defensible** (setiap keputusan sudah documented dengan justifikasi konkret, bukan intuisi).
