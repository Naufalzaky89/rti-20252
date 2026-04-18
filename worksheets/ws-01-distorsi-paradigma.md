Nama Peneliti    : Naufal zaky
Tanggal          : 18 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: 
     "Akurat pada dataset apa? Apakah data latih dan data uji dipisah 
     secara ketat, atau ada kebocoran data (data leakage)? 
     Apakah kelas normal dan anomali seimbang di dataset tersebut?"
   - Data yang dibutuhkan untuk verifikasi:
     Distribusi kelas (rasio normal vs anomali), ukuran dan sumber 
     dataset, metode split train/test, dan nilai precision-recall 
     selain akurasi.

2. Posisi paradigma:
   - Pendekatan: [x] Design Science Research + [x] Positivis (Mixed)
   - Alasan: 
     Riset IoT anomaly detection membangun artefak (model ML/DL) 
     sekaligus menguji hipotesis terukur seperti "apakah XGBoost+LSTM 
     meningkatkan F1-score ≥5% dibanding baseline LSTM?" — 
     keduanya saling melengkapi.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: 
     Dataset benchmark (misal: TON_IoT, CICIDS) dianggap mewakili 
     kondisi nyata, padahal lalu lintas jaringan IoT sangat 
     bergantung pada vendor dan lingkungan deployment.
   - Sumber bias potensial: 
     Class imbalance (anomali jauh lebih sedikit dari data normal), 
     sehingga model bisa terlihat "akurat" meski hampir tidak pernah 
     mendeteksi anomali sama sekali.
   - Langkah mitigasi: 
     Gunakan F1-score, precision, dan recall sebagai metrik utama 
     (bukan hanya akurasi); terapkan teknik oversampling (SMOTE) 
     atau threshold tuning.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: 
     Hasil eksperimen pada data uji (test set) tidak akan diubah; 
     hyperparameter tidak akan di-tune ulang setelah melihat 
     performa test set.
   - Batasan yang diakui sejak awal: 
     Model hanya diuji pada dataset benchmark statis, bukan    
     lingkungan IoT nyata secara real-time.
     📝 Latihan 1 — Identifikasi Distorsi
Paper yang Dipilih

Judul: An Effective Method for Anomaly Detection in Industrial Internet of Things Using XGBoost and LSTM
Penulis (Tahun): Zhen Chen, ZhenWan Li, Jia Huang, ShengZheng Liu, HaiXia Long (2024)
Sumber/DOI: https://doi.org/10.1038/s41598-024-74822-6 (Scientific Reports, Nature — Open Access)

Klaim utama paper: Metode hybrid XGBoost (untuk seleksi fitur) + LSTM (untuk deteksi) menghasilkan performa deteksi anomali yang lebih tinggi dibanding metode baseline pada dataset IIoT.

Tabel Analisis Research Trust Model
TahapApa yang Dilakukan PaperPotensi DistorsiReality → DataMenggunakan dataset benchmark IIoT yang tersedia publik (bukan sensor industri nyata secara live)Dataset statis tidak merepresentasikan dinamika lalu lintas IoT nyata yang terus berubah; kondisi jaringan satu vendor bisa sangat berbedaData → ProcessingXGBoost digunakan untuk seleksi fitur: fitur dengan importance di atas threshold dipertahankan, sisanya dibuangThreshold seleksi fitur dipilih secara eksperimental — jika threshold di-tune berulang kali sambil melihat hasil akhir, ini berpotensi menjadi data leakage atau overfitting pada dataset tertentuProcessing → AnalysisLSTM dilatih untuk mendeteksi pola temporal anomali pada fitur yang sudah diseleksiClass imbalance: data anomali jauh lebih sedikit dari data normal di dunia nyata; jika tidak ditangani dengan baik, model bisa bias ke kelas mayoritas (normal) dan tetap tampak "akurat"Analysis → InferencePerforma dibandingkan dengan beberapa baseline (misal: LSTM murni, metode lain) menggunakan metrik akurasi, precision, recall, F1Pemilihan baseline yang "lemah" (strawman comparison) bisa membuat metode baru terlihat lebih unggul; jika baseline tidak di-tune secara adil, perbandingan menjadi tidak setaraInference → KnowledgeDisimpulkan bahwa XGBoost+LSTM efektif dan direkomendasikan untuk deteksi anomali IIoT secara umumGeneralisasi berlebihan: kesimpulan diambil dari satu atau beberapa dataset benchmark saja, lalu digeneralisasi ke seluruh domain IIoT padahal performa bisa sangat berbeda di lingkungan deployment yang berbeda

Distorsi paling besar di tahap: Inference → Knowledge
Dua distorsi spesifik yang teridentifikasi:

Class Imbalance Bias (tahap Processing → Analysis): Dataset IIoT cenderung sangat tidak seimbang — data normal jauh mendominasi. Jika paper hanya melaporkan akurasi keseluruhan tanpa menekankan precision/recall per kelas, model yang hampir tidak pernah mendeteksi anomali pun bisa mendapat akurasi >90%. Ini adalah distorsi construct validity — metrik yang digunakan tidak sepenuhnya mengukur apa yang diklaim (kemampuan mendeteksi anomali).
Dataset-Specific Overgeneralization (tahap Inference → Knowledge): Kesimpulan "metode ini efektif untuk IIoT" dibangun di atas 1–2 dataset benchmark yang bersifat statis dan mungkin tidak merepresentasikan jaringan IoT vendor berbeda, protokol berbeda, atau kondisi serangan baru. Ini adalah ancaman terhadap external validity — temuan mungkin tidak bisa digeneralisasi ke konteks nyata yang lebih luas.


⚖️ Latihan 2 — Analisis Kasus Etika
Skenario: Peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.
PerspektifAnalisisKejujuran ilmiahMenghapus outlier hanya karena membuat hasil tidak signifikan adalah bentuk data manipulation — ini melanggar prinsip kejujuran ilmiah. Keputusan untuk menghapus atau mempertahankan outlier harus dibuat sebelum melihat dampaknya terhadap signifikansi. Jika keputusan penghapusan dibuat sesudah melihat hasil, ini termasuk kategori HARKing dalam bentuk manipulasi data. Solusi yang benar: laporkan kedua versi (dengan dan tanpa outlier) beserta justifikasi statistik yang jelas (misalnya: uji Grubbs, Z-score) mengapa outlier tersebut dapat dianggap tidak valid secara prosedural.TransparansiJika outlier dihapus, alasan penghapusannya wajib didokumentasikan secara eksplisit di bagian metodologi — bukan sekadar "data dibersihkan." Transparansi juga menuntut peneliti mengungkapkan bahwa hasil berubah secara signifikan setelah penghapusan; pembaca berhak mengetahui hal ini untuk mengevaluasi kekuatan klaim. Menyembunyikan informasi ini adalah bentuk distorsi yang disengaja.Peer reviewReviewer yang baik akan menanyakan: "Apa kriteria penghapusan outlier yang digunakan, dan apakah kriteria ini ditetapkan sebelum analisis?" Jika peneliti tidak bisa menjawab dengan protokol yang jelas dan terdokumentasi sejak awal, maka penghapusan tersebut tidak dapat dipertahankan secara ilmiah. Paper seharusnya tidak lolos peer review jika outlier dihapus tanpa justifikasi metodologis yang kuat dan pre-defined.
Keputusan akhir dan justifikasi:

Outlier tidak boleh dihapus semata-mata untuk mendapatkan hasil yang signifikan. Keputusan yang etis adalah: (1) laporkan hasil lengkap dengan outlier sebagai hasil utama, (2) sertakan analisis sensitivitas (sensitivity analysis) tanpa outlier sebagai temuan tambahan dengan justifikasi statistik yang transparan, dan (3) akui bahwa hasil tanpa outlier hanya bersifat eksploratif. Hasil yang tidak signifikan pun merupakan kontribusi ilmiah yang valid — ia memberi tahu komunitas riset bahwa metode tersebut tidak bekerja secara robust di semua kondisi data. Menyembunyikannya justru merugikan akumulasi pengetahuan ilmiah.


🔭 Latihan 3 — Posisi Paradigma
Topik riset: Deteksi Anomali pada Data Sensor IoT Menggunakan Model Deep Learning Hybrid
KriteriaPositivisInterpretivisDesign Science Research (DSR)Kesesuaian dengan topik (1–5)4 — Topik sangat kuantitatif; ada hipotesis terukur seperti "apakah model hybrid XGBoost+LSTM meningkatkan F1-score ≥5% vs baseline?" yang bisa diuji dengan eksperimen terkontrol1 — Topik ini tidak menyelidiki makna, persepsi, atau konteks sosial; pendekatan kualitatif tidak relevan untuk masalah teknis deteksi anomali5 — Inti riset adalah membangun artefak (arsitektur model hybrid) untuk membuktikan proposisi bahwa desain tersebut meningkatkan kemampuan deteksi; DSR sangat dominan di bidang iniJenis data yang dikumpulkanMetrik numerik: akurasi, precision, recall, F1-score, AUC-ROC; log eksperimen terkontrol; hasil perbandingan antar modelWawancara dengan operator sistem IoT, observasi kualitatif penggunaan sistem — tidak relevan untuk riset teknis iniHasil pengujian artefak (model) pada beberapa dataset; komparasi kinerja dengan baseline; analisis ablation study (kontribusi tiap komponen)Limitasi paradigmaEksperimen terkontrol di lab/dataset benchmark mungkin tidak mencerminkan kondisi sensor IoT nyata yang noisy dan dinamis; sulit mengontrol semua confounding variable di deployment nyataTidak mampu menghasilkan klaim yang terukur dan dapat direplikasi; tidak cocok untuk mengevaluasi performa model secara objektifArtefak (model) yang dibangun bisa terlalu disesuaikan dengan dataset tertentu; risiko bahwa "kontribusi pengetahuan" hanya berlaku untuk konfigurasi spesifik yang diuji
Paradigma yang dipilih: Design Science Research (DSR) dengan elemen Positivis
Alasan: Riset deteksi anomali IoT pada intinya adalah membangun sebuah artefak (model/arsitektur ML/DL), namun artefak tersebut bukan tujuan akhir — ia digunakan untuk menjawab pertanyaan riset yang falsifiable: "Apakah arsitektur hybrid XGBoost+LSTM terbukti meningkatkan recall deteksi anomali pada data sensor IIoT dibandingkan baseline dengan peningkatan minimal 5%?" DSR memberikan kerangka untuk proses build-evaluate yang iteratif, sementara pendekatan Positivis memastikan evaluasi dilakukan secara objektif dengan eksperimen terkontrol dan metrik yang terukur. Kombinasi keduanya adalah standar yang paling umum dan paling kuat untuk riset di bidang ini.

💭 Refleksi
Pertanyaan:

Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

Jawaban:
Sebelum memahami Research Trust Model, angka "95% akurat" terasa langsung meyakinkan — angka besar identik dengan metode yang bagus. Distorsi dalam rantai riset tidak terlihat karena tidak ada kerangka berpikir untuk mencarinya.
Setelah memahami enam tahap transformasi dan jenis-jenis validitas, berikut pertanyaan yang sekarang akan diajukan secara sistematis saat membaca paper IoT:

Tentang data (Reality → Data): Dari mana dataset berasal? Apakah merupakan data nyata atau simulasi? Seberapa representatif distribusi kelas anomali vs normal-nya?
Tentang processing: Apakah normalisasi dan seleksi fitur dilakukan sebelum split train/test, atau sesudah? Jika sesudah, ada potensi data leakage.
Tentang metrik (Construct Validity): Mengapa hanya melaporkan akurasi? Pada dataset yang imbalanced, akurasi bisa menyesatkan — di mana nilai precision, recall, dan F1-score per kelas?
Tentang baseline (Internal Validity): Apakah baseline di-tune secara adil dengan usaha yang sama seperti metode yang diusulkan, atau sengaja dibiarkan lemah?
Tentang generalisasi (External Validity): Diuji pada berapa dataset? Apakah kondisi dataset mewakili lingkungan IoT nyata, atau hanya satu benchmark standar yang sudah "dikenal" komunitas riset?
