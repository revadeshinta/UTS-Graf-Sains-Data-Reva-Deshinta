# UTS Graf Sains Data

**Nama:** Reva Deshinta Isyana  
**NIM:** 23031554153
**Mata Kuliah:** Graf Sains Data
**Kelas:** 2023D

## Deskripsi Proyek

Proyek ini merupakan tugas Ujian Tengah Semester (UTS) mata kuliah Graf Sains Data dengan menggunakan dataset **RetailRocket**.

Analisis dilakukan menggunakan Python dan Neo4j untuk membangun graf interaksi antara Visitor dan Item, menghitung kemiripan antar-Visitor menggunakan Cosine Similarity, serta menghasilkan rekomendasi Item menggunakan metode User-Based Collaborative Filtering dengan K-Nearest Neighbors (KNN).

## Dataset

Dataset yang digunakan adalah RetailRocket, khususnya file `events.csv` yang berisi riwayat interaksi pengguna dengan produk.

Data dibagi menjadi dua periode:

| Dataset | Periode | Jumlah Event | Kegunaan |
|---|---|---:|---|
| P1 (Training) | 1–14 Juli 2015 | 309.637 | Pembentukan graf dan sistem rekomendasi |
| P2 (Testing) | 15–21 Juli 2015 | 148.197 | Evaluasi rekomendasi |

File dataset yang disertakan:
- `retailrocket_P1_training.csv`
- `retailrocket_P2_testing.csv`

## Metode Analisis

### 1. Pembentukan Graf Neo4j

Data interaksi pada periode P1 diimpor ke Neo4j dengan dua jenis node, yaitu `Visitor` dan `Item`.

Relationship yang digunakan meliputi `VIEWED`, `ADDED_TO_CART`, dan `BOUGHT`.

Graf P1 terdiri dari 171.802 node Visitor, 83.507 node Item, dan 309.637 relationship aktivitas.

### 2. Vector Space Model (VSM)

Interaksi Visitor dan Item direpresentasikan menggunakan sparse matrix untuk membentuk VSM Visitor dan VSM Item.

VSM Visitor memiliki ukuran 171.802 × 83.507, sedangkan VSM Item memiliki ukuran 83.507 × 171.802.

### 3. Cosine Similarity

Cosine Similarity digunakan untuk mengukur kemiripan antar-Visitor berdasarkan Item yang pernah diakses.

Hasil kemiripan antar-Visitor juga direpresentasikan dalam Neo4j menggunakan relationship `SIMILAR_TO`.

### 4. Rekomendasi User-Based KNN

Sistem rekomendasi menggunakan pendekatan User-Based Collaborative Filtering dengan nilai `k = 5`.

Lima tetangga dipilih berdasarkan Cosine Similarity positif tertinggi, dengan syarat memiliki minimal satu Item yang belum diakses Visitor target.

Kandidat Item kemudian diberi skor berdasarkan jumlah nilai similarity tetangga yang mengaksesnya.

### 5. Evaluasi Hit@5 dan NDCG@5

Evaluasi dilakukan menggunakan data P2 untuk membandingkan lima rekomendasi teratas dengan Item baru yang benar-benar diakses Visitor target.

Hasil evaluasi untuk Visitor `957260`:

| Metrik | Hasil |
|---|---|
| Hit@5 | 0 |
| NDCG@5 | 0.0 |

Hasil tersebut menunjukkan bahwa tidak ada Item relevan yang ditemukan dalam lima rekomendasi teratas untuk Visitor yang diuji.

## Struktur File

```text
UTS-Graf-Sains-Data/
├── UTSGSD_Final.ipynb
├── retailrocket_P1_training.csv
├── retailrocket_P2_testing.csv
├── Graf_Sebelum_Similarity.png
├── Graf_Sesudah_Similarity.png
└── README.md
```

## Teknologi yang Digunakan

- Python
- Jupyter Notebook
- Neo4j
- Pandas
- NumPy
- SciPy
- Scikit-learn
- NetworkX
- Matplotlib

## Dokumentasi

Seluruh kode program, hasil visualisasi, proses analisis, dan penjelasan terdapat dalam notebook **`UTSGSD_Final.ipynb`**.

Dataset P1 dan P2 disertakan agar pembagian data dan analisis dapat diperiksa kembali.

## Kesimpulan

Proyek ini menunjukkan penerapan graf untuk merepresentasikan interaksi pengguna dan produk serta penggunaan Cosine Similarity dan User-Based KNN untuk menghasilkan rekomendasi Item.

Evaluasi terhadap satu Visitor menghasilkan Hit@5 dan NDCG@5 sebesar 0, sehingga sistem belum berhasil memprediksi Item relevan untuk Visitor tersebut. Hasil ini belum menggambarkan performa keseluruhan sistem rekomendasi.
