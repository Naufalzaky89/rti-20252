# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---
```
## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: ____________________

Apakah integrasi fitur kontekstual (promo dan hari libur) pada arsitektur LSTM dapat menurunkan nilai Mean Absolute Percentage Error (MAPE) secara signifikan dibandingkan dengan model Vanilla LSTM pada dataset ritel menengah?


---
 
 Latihan 1 — Variable-to-Component Mapping
 
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|------------------------------|
| Variasi Fitur Input | IV | Feature Engineering Pipeline | Mengaktifkan/menonaktifkan penggabungan (concatenation) vektor fitur eksternal ke dalam matriks data sekuensial. |
| Nilai Error Peramalan (MAPE & RMSE) | DV | Metrics Logger & Visualization Dashboard | Fungsi matematika berbasis Scikit-Learn mengekstrak nilai keluaran model dan menghitung nilai MAPE-nya secara otomatis. |
| Hyperparameter Model | CV | Hyperparameter Config Layer | Mengunci arsitektur jaringan (jumlah hidden layers dan tingkat dropout) di dalam file konfigurasi terpisah agar tidak berubah selama uji coba. |
 
Apakah semua variabel bisa di-map?  Ya
 
Justifikasi: Arsitektur sistem dirancang secara modular — memisahkan jalur data preparation, pemodelan (core engine), dan evaluasi — sehingga mempermudah pemetaan setiap variabel riset.
 
---
 
 Latihan 2 — Evaluasi 4 Prinsip Desain Sistem
 
| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|--------------------|
| Traceability |  Lulus | Alur kode program mengalir searah dari penyiapan data (IV & CV) menuju fungsi pelatihan hingga menghasilkan metrik pengujian (DV). |
| Modularity |  Lulus | Komponen feature loader eksternal terpisah dari blok kode utama algoritma LSTM, sehingga data promo bisa dicabut tanpa merusak program. |
| Controllability |  Lulus | Seluruh parameter kontrol seperti batasan waktu, learning rate, dan ukuran sliding window dikumpulkan di satu file konfigurasi (`config.json`). |
| Measurability |  Lulus | Setiap kali iterasi pelatihan (epoch) atau pengujian selesai, sistem langsung memicu fungsi kalkulasi skor akurasi dan menyimpannya secara permanen. |
 
Prinsip paling sulit dipenuhi:Controllability
 
> Strategi Mengatasi: Sangat menantang untuk mengontrol kebersihan data di lapangan agar benar-benar konstan (CV), karena terkadang ada anomali tak terduga seperti toko tiba-tiba tutup karena kendala teknis operasional. Strateginya adalah membuat modul penanganan data (*data cleaning layer*) yang secara otomatis menyaring atau mengimputasi (impute) data kosong berdasarkan pola rata-rata hari sejenis sebelum data dimasukkan ke model.
 
---
 
 Latihan 3 — Ablation Study Planning
 
> Sistem ini memiliki 3 komponen fitur utama:
> - A — Fitur Histori Penjualan
> - B — Fitur Promo Internal
> - C — Fitur Hari Libur Nasional
 
| Kondisi | Komponen A (Histori) | Komponen B (Promo) | Komponen C (Libur) | Hasil yang Diharapkan |
|---------|----------------------|--------------------|--------------------|----------------------|
| Full |  Aktif | Aktif |  Aktif | Nilai MAPE terendah (akurasi paling optimal secara menyeluruh). |
| – B |  Aktif |  Non-Aktif |  Aktif | Akurasi menurun pada hari kerja biasa yang memiliki program diskon mendadak. |
| – C |  Aktif |  Aktif |  Non-Aktif | Akurasi anjlok drastis pada periode libur panjang/Lebaran (peak season error). |
| Baseline |  Aktif |  Non-Aktif |  Non-Aktif | Model Vanilla LSTM standar (hanya membaca pola masa lalu tanpa tahu situasi pasar). |
 
Komponen yang diprediksi paling berkontribusi:** Komponen C (Fitur Hari Libur Nasional)
 
alsaaan: Di Indonesia, siklus hari libur keagamaan (seperti Ramadan dan Lebaran) menciptakan lonjakan volume belanja (demand spike) hingga berkali-kali lipat dari hari biasa. Jika fitur ini dihilangkan, model LSTM akan mengalami kebingungan karena menganggap lonjakan tersebut sebagai gangguan acak (noise), bukan sebagai pola berulang tahunan.
 
---
 
  Refleksi
 
 Risiko terbesar jika membangun sistem riset seperti produk komersial (monolitik dan langsung kaya fitur) adalah munculnya efek bias tersembunyi. Ketika eksperimen dilakukan dan hasilnya buruk atau justru sangat bagus, peneliti akan kesulitan melacak komponen mana yang sebenarnya membawa dampak tersebut karena semua kode saling terikat erat (tightly coupled).
 
> Arsitektur modular sangat krusial dalam dunia riset karena mengizinkan kita melakukan Isolasi Variabel. Kita bisa secara adil membandingkan performa dengan skema mencabut satu komponen (seperti pada Ablation Study) tanpa perlu merombak atau menulis ulang baris kode sistem dari awal. Hal ini menjamin transparansi, keadilan pengujian, dan aspek reprodusibilitas riset.
 
