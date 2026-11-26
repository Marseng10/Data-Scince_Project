# Analisis Pola dan Prediksi Magnitudo Gempa Bumi

Proyek ini menganalisis karakteristik kejadian gempa bumi signifikan secara global dan mengembangkan model regresi untuk mengestimasi magnitudo berdasarkan karakteristik kejadian seismik yang telah tercatat. Analisis dilakukan menggunakan Python dan mengikuti kerangka kerja **CRISP-DM**.

> **Catatan:** Proyek ini merupakan estimasi retrospektif berdasarkan data gempa yang sudah tercatat, bukan sistem untuk meramalkan kapan atau di mana gempa akan terjadi dan bukan sistem peringatan dini (*early warning system*).

## Ringkasan Proyek

Dataset yang digunakan adalah **Significant Earthquakes, 1965–2016**, yang bersumber dari Kaggle / USGS Earthquake Database. Analisis difokuskan pada kejadian bertipe `Earthquake` dengan target prediksi berupa kolom `Magnitude`.

Ruang lingkup pekerjaan meliputi:

1. **Exploratory Data Analysis (EDA):** mengeksplorasi distribusi magnitudo dan kedalaman, pola kejadian berdasarkan waktu, persebaran episentrum, serta hubungan antarvariabel.
2. **Data Understanding:** memeriksa struktur atribut, tipe data, missing values, duplikasi, nilai tidak valid, outlier, potensi bias, dan keterbatasan dataset.
3. **Data Preparation:** melakukan pemilihan fitur, pembentukan atribut waktu, pembersihan data, pembagian data secara kronologis, serta preprocessing.
4. **Modeling:** membandingkan `DummyRegressor`, `LinearRegression`, dan `Ridge Regression` dengan beberapa nilai alpha.
5. **Evaluation:** mengevaluasi model menggunakan MAE, RMSE, dan R² pada data validasi dan pengujian.

### Fitur dan Target

| Jenis | Atribut |
|---|---|
| Fitur | `Latitude`, `Longitude`, `Depth`, `Depth Seismic Stations`, `Year`, `Month`, `Hour` |
| Target | `Magnitude` |

### Pembagian Data

Data dibagi berdasarkan periode waktu untuk menghindari kebocoran informasi masa depan (*data leakage*).

| Subset | Periode | Jumlah data |
|---|---:|---:|
| Training | 1965–2000 | 15.040 |
| Validation | 2001–2010 | 5.176 |
| Testing | 2011–2016 | 3.013 |
| **Total** | **1965–2016** | **23.229** |

### Hasil Utama

Model yang dipilih berdasarkan evaluasi validasi adalah **Ridge Regression dengan alpha = 1,0**.

| Evaluasi | MAE | RMSE | R² |
|---|---:|---:|---:|
| Validation | 0,2862 | 0,3793 | 0,1997 |
| Testing | 0,3224 | 0,4413 | -0,0170 |

Hasil pengujian menunjukkan bahwa kemampuan generalisasi model masih terbatas. Nilai R² testing yang negatif menunjukkan bahwa model belum mampu menjelaskan variasi magnitudo pada periode pengujian dengan baik. Model juga cenderung meremehkan magnitudo pada kejadian gempa sangat kuat.

## Anggota Kelompok dan Kontribusi

| No. | Nama | NIM | Kontribusi |
|---:|---|---|---|
| 1 | Lathiva Safina Almasea | 123240226 | Mengerjakan eksplorasi data (EDA), termasuk analisis distribusi magnitudo dan kedalaman, pola kejadian gempa berdasarkan waktu, persebaran geografis episentrum, serta visualisasi dan interpretasi hasil eksplorasi. |
| 2 | Faiz Maulana B. | 123240249 | Mengerjakan Data Understanding, meliputi identifikasi sumber dan struktur dataset, pemeriksaan tipe data, missing values, duplikasi, nilai tidak valid, outlier, serta analisis kualitas dan keterbatasan data. |
| 3 | M. Ahsan R. S. | 123240246 | Mengerjakan Data Preparation, meliputi pembersihan data, pembentukan fitur waktu, pemilihan fitur dan target, penanganan missing values, preprocessing, serta pembagian data secara kronologis menjadi training, validation, dan testing. |
| 4 |  Karina Sulistya D | 123240227 | Mengerjakan pemodelan dan evaluasi, meliputi pembangunan serta perbandingan Dummy Regressor dan Ridge Regression, pemilihan parameter alpha berdasarkan data validasi, evaluasi MAE/RMSE/R², analisis kesalahan prediksi, dan penyusunan kesimpulan. |

*Pembagian kontribusi di atas merupakan rancangan pembagian tugas yang disusun berdasarkan tahapan pekerjaan dalam notebook. Sesuaikan kembali apabila pelaksanaan tugas aktual setiap anggota berbeda.*

## Sumber Data

- **Nama dataset:** Significant Earthquakes, 1965–2016.
- **Sumber yang dicantumkan pada notebook:** Kaggle / USGS Earthquake Database.
- **Periode data:** 1965–2016.
- **Cakupan:** kejadian gempa bumi signifikan global, dengan data yang digunakan dalam analisis dibatasi pada tipe kejadian `Earthquake` dan magnitudo signifikan (sekitar M ≥ 5,5).

Pastikan file dataset CSV yang digunakan merupakan file yang sesuai dengan dataset tersebut. Notebook menggunakan nama file input `database.csv` pada bagian Data Understanding dan `database 2.csv` pada bagian EDA. Jika hanya memiliki satu file dataset, samakan nama file pada pemanggilan `pd.read_csv()` di notebook atau sediakan kedua file dengan isi yang sesuai.

## Teknologi dan Library

Proyek dikembangkan menggunakan Python dengan library berikut:

- `pandas` — membaca, membersihkan, dan mengolah data.
- `numpy` — komputasi numerik.
- `matplotlib` dan `seaborn` — visualisasi data.
- `scikit-learn` — preprocessing, pemodelan regresi, dan evaluasi.
- `statsmodels` — analisis statistik.

## Panduan Menjalankan Proyek

### 1. Persiapan

Pastikan Python telah terpasang. Disarankan menggunakan virtual environment agar dependensi proyek terisolasi.

Clone repository:

```bash
git clone <URL_REPOSITORY>
cd <NAMA_FOLDER_REPOSITORY>
```

Atau unduh repository sebagai ZIP, lalu ekstrak ke folder kerja.

### 2. Siapkan Dataset

Letakkan file dataset CSV di folder yang sama dengan notebook:

```text
nama-folder-proyek/
├── AnalisisPoladanPrediksiMagnitudoGempaBumi_Lanjutan.ipynb
├── database.csv
└── database 2.csv
```

Nama file harus disesuaikan dengan nama yang dipanggil pada kode notebook. Saat ini notebook memanggil `database 2.csv` pada bagian EDA dan `database.csv` pada bagian Data Understanding.

### 3. Buat Virtual Environment (Opsional)

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Instal Library

Jalankan perintah berikut pada terminal:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels jupyter
```

### 5. Jalankan Notebook

Dari folder proyek, jalankan:

```bash
jupyter notebook
```

Buka file `AnalisisPoladanPrediksiMagnitudoGempaBumi_Lanjutan.ipynb`, kemudian jalankan sel secara berurutan dari bagian awal hingga akhir (*Run All*).

Alternatifnya, notebook dapat dibuka menggunakan Visual Studio Code dengan ekstensi Jupyter yang sudah terpasang.

### 6. Periksa Hasil

Notebook menghasilkan proses eksplorasi, pemeriksaan kualitas data, preprocessing, pelatihan model, evaluasi, dan visualisasi. Beberapa nama file keluaran yang ditulis oleh notebook antara lain:

- `gempa_clean.csv`
- `dataset_gempa_final.csv`
- `gambar_u_korelasi_fitur_magnitude.png`

Pastikan folder tempat notebook dijalankan memiliki izin untuk membaca dataset dan menyimpan file keluaran.

## Catatan dan Keterbatasan

1. Dataset hanya mencakup gempa signifikan pada periode 1965–2016 sehingga tidak mewakili seluruh aktivitas gempa, khususnya gempa bermagnitudo kecil.
2. Atribut `Depth Seismic Stations` memiliki banyak nilai kosong, terutama pada periode historis. Penanganan missing value dilakukan melalui imputasi median yang dipelajari dari data training.
3. Pembagian training, validation, dan testing dilakukan berdasarkan urutan tahun. Parameter preprocessing dipelajari dari training untuk menghindari *data leakage*.
4. Hasil pengujian memperlihatkan bahwa model masih kesulitan mengestimasi gempa bermagnitudo sangat besar.
5. Hasil proyek tidak boleh digunakan sebagai prediksi operasional kejadian gempa atau sebagai dasar sistem peringatan dini.

---

**Dokumen proyek:** Analisis Pola dan Prediksi Magnitudo Gempa Bumi Berdasarkan Karakteristik Kejadian Seismik Global.
