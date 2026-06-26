# Matriks Literatur — Peningkatan Akurasi Peramalan Persediaan Ritel

Matriks ini memetakan paper dan referensi yang relevan dengan penelitian tentang peningkatan akurasi peramalan persediaan ritel melalui integrasi fitur kontekstual pada model deep learning LSTM.

## Tabel Matriks Literatur

| No | Penulis | Tahun | Judul | Fokus Utama | Metodologi | Gap / Keterbatasan | Jurnal / Sumber |
|---|---|---|---|---|---|---|---|
| 1 | Rahmansyah, S., dkk. | 2023 | Implementasi Algoritma Long Short-Term Memory (LSTM) Untuk Prediksi Persediaan Barang pada Toko Retail | Peramalan stok barang menggunakan model deret waktu | LSTM univariat murni, dataset POS real | Mengabaikan faktor luar seperti promo internal toko; eror tinggi saat lonjakan permintaan | Jurnal Teknologi Informasi dan Ilmu Komputer (JTIIK), Vol. 10, No. 2, hal. 345-352 |
| 2 | Sutrisno & Budiono | 2024 | Perbandingan Algoritma LSTM dan ARIMA dalam Peramalan Stok Barang | Evaluasi performa LSTM vs ARIMA pada peramalan stok | Komparasi RMSE, MAE; analisis tren musiman | Akurasi menurun < 70% pada periode puncak karena tidak terintegrasi dengan kalender hari libur dan keagamaan lokal | Jurnal Nasional Teknik Elektro dan Teknologi Informasi (JNTETI), Vol. 13, No. 1, hal. 58-66 |
| 3 | Putra, D., dkk. | 2024 | Penerapan Hybrid Machine Learning untuk Manajemen Persediaan UKM | Optimasi safety stock dan reorder point pada UKM | Kombinasi clustering (K-Means) dan regresi linear | Data cenderung homogen dan terisolasi; belum menguji kekuatan model deep learning dalam menangani fluktuasi non-linear kompleks | Jurnal Teknologi dan Sistem Komputer, Vol. 12, No. 3, hal. 180-188 |
| 4 | Chollet, F. | 2021 | Deep Learning with Python, Second Edition | Teori dasar dan implementasi RNN & LSTM untuk berbagai kasus | Buku referensi fundamental tentang arsitektur jaringan saraf | Fokus pengenalan teks dan deret waktu global; tidak memuat pipeline rekayasa fitur (feature engineering) khusus retail lokal | Manning Publications |
| 5 | Hyndman, R. J. & Athanasopoulos, G. | 2021 | Forecasting: Principles and Practice (3rd ed.) | Metodologi forecasting deret waktu secara komprehensif | Teori statistik forecasting klasik; evaluasi metrik MAPE, MAE, MSE | Didominasi pendekatan statistik tradisional (ARIMA, ETS); tidak mengeksplorasi pembobotan multivariabel pada model deep learning | O'Reilly Media |

## Pemetaan Topik vs. Referensi

| Topik | Referensi yang Relevan | Catatan |
|---|---|---|
| **LSTM untuk forecasting deret waktu** | Chollet (2021) [4], Rahmansyah dkk. (2023) [1] | Dasar teori dan aplikasi LSTM pada retail |
| **Integrasi fitur kontekstual** | *Gap area* — belum ada studi spesifik | Menjadi kontribusi penelitian ini |
| **Pengaruh promosi pada permintaan** | Rahmansyah dkk. (2023) [1], Sutrisno & Budiono (2024) [2] | Keduanya mengidentifikasi masalah namun belum menyelesaikan |
| **Kalender dan momen khusus** | Sutrisno & Budiono (2024) [2], Hyndman & Athanasopoulos (2021) [5] | Pentingnya musim dan kalender dalam forecasting |
| **Evaluasi metrik performa** | Hyndman & Athanasopoulos (2021) [5], Sutrisno & Budiono (2024) [2] | MAPE, RMSE, MAE sebagai standar evaluasi |
| **Uji signifikansi statistik** | Hyndman & Athanasopoulos (2021) [5] | Metodologi validasi hasil namun belum banyak diterapkan |
| **Hybrid machine learning** | Putra dkk. (2024) [3] | Pendekatan kombinasi namun terbatas pada model sederhana |

## Gap Penelitian yang Diidentifikasi

Berdasarkan matriks literatur di atas, gap penelitian yang teridentifikasi adalah:

### 1. Belum Ada Integrasi Fitur Kontekstual Langsung pada First-Layer LSTM
- Literatur existing (Rahmansyah dkk., 2023; Sutrisno & Budiono, 2024) mengidentifikasi masalah bahwa model univariat mengalami distorsi akurasi saat ada lonjakan permintaan.
- Namun, belum ada penelitian yang secara langsung menyuntikkan fitur biner kontekstual (promo internal dan hari libur) ke dalam urutan matriks input pertama LSTM.

### 2. Distorsi Model Univariat pada Dinamika Pasar Riil
- Model univariat murni mengisolasi sistem dari dinamika pasar, mengakibatkan lonjakan permintaan diperlakukan sebagai noise acak.
- Akibatnya, MAPE melonjak di atas 18-20% pada periode puncak dan post-puncak.

### 3. Ketiadaan Uji Signifikansi Statistik Inferensial
- Penelitian terdahulu hanya melaporkan penurunan nilai metrik mentah (raw metrics).
- Belum banyak yang menggunakan uji statistik (misal: Wilcoxon Signed-Rank Test) untuk membuktikan apakah penurunan eror merupakan hasil intervensi model atau sekadar variasi acak.

### 4. Keterbatasan Modularisasi dan Studi Ablasi
- Arsitektur forecasting existing umumnya bersifat monolitik.
- Sulit melakukan ablation study yang adil untuk mengukur pengaruh masing-masing fitur secara terpisah.

### 5. Dataset Berukuran Sempit dan Periode Pengujian Pendek
- Pengujian model existing sering dibatasi pada periode < 6 bulan.
- Penelitian ini menggunakan data 3 tahun penuh (2023-2025) untuk generalisasi lebih baik.

## Kesimpulan Tinjauan Pustaka

Literatur existing memberikan fondasi teori LSTM dan forecasting yang kuat, namun masih terdapat celah signifikan dalam:
- integrasi sistematis fitur kontekstual ke dalam arsitektur neural network,
- validasi statistik inferensial terhadap manfaat intervensi model,
- modularisasi pipeline eksperimen untuk studi ablasi yang ketat.

Penelitian ini bertujuan mengisi celah tersebut melalui arsitektur Contextual-LSTM yang termodularisasi dan evaluasi rigor dengan uji signifikansi statistik.