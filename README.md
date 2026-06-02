# Smart Playlist Generator: Pendekatan Hibrida (Audio DNA & Niche Genre)

Proyek ini merupakan implementasi gabungan dari **Teknologi Big Data** dan **Kecerdasan Bisnis (Business Intelligence)**. Sistem ini mengekstrak fitur hibrida dari ratusan ribu lagu untuk menghasilkan rekomendasi playlist otomatis yang cerdas tanpa bergantung pada data riwayat interaksi pengguna (*zero user history*), sehingga secara efektif mampu menyelesaikan masalah *Cold-Start* pada platform streaming musik.

## Alur & Arsitektur Sistem

Sistem rekomendasi ini bekerja melalui 4 fase pipeline utama:

1. **ETL & Pembersihan Data (PySpark):** Memproses dataset mentah berskala besar (550K lagu), melakukan deduplikasi, pembersihan data kosong (*null values*), dan konvrensi tipe data.
2. **Feature Engineering (PySpark & Scikit-Learn):** * Standarisasi 8 dimensi audio (*danceability, energy, tempo, valence*, dll) menggunakan `StandardScaler`.
   * Klasifikasi dan pemecahan 754 label genre unik menggunakan `MultiLabelBinarizer` (*One-Hot Encoding*).
3. **Hybrid Feature Matrix:** Menggabungkan matriks audio dan matriks genre menggunakan rumus pembobotan hibrida $\alpha$ (Audio) dan $\beta$ (Genre) secara seimbang (50:50) menjadi satu matriks terpadu berdimensi 762.
4. **Mesin Rekomendasi (Cosine Similarity):** Mengukur kedekatan jarak geometris antar vektor lagu untuk menyajikan top-N lagu paling identik berdasarkan lagu referensi (*seed song*) disertai filter anti-varian (Remix/Acoustic/Live).

---

## Panduan Instalasi Lokal

### 1. Prasyarat Sistem (Prerequisites)
Sebelum membuat *virtual environment*, pastikan perangkat Anda sudah terpasang **Python (versi 3.10 - 3.12 direkomendasikan)** dan **Java Runtime Environment (JRE/JDK versi 8 atau 11)** yang diwajibkan oleh Apache Spark untuk memproses data.

### 2. Setup Virtual Environment & Aktivasi

Buka terminal (Linux/macOS) atau Command Prompt/PowerShell (Windows) di dalam direktori utama proyek Anda, lalu jalankan perintah sesuai OS Anda:

#### 🐧 Linux & 🍏 macOS
```bash
# 1. Buat virtual environment baru
python3 -m venv .venv
```
```bash
# 2. Aktifkan environment
source .venv/bin/activate
```
```bash
# 3. Upgrade package manager internal venv
pip install --upgrade pip
```
### Windows (PowerShell / CMD)
```bash
# 1. Buat virtual environment baru
python -m venv .venv
```
```bash
# 2. Aktifkan environment (Pilih salah satu sesuai aplikasi terminal Anda)
# Jika menggunakan PowerShell:
.venv\Scripts\Activate.ps1
# Jika menggunakan Command Prompt (CMD):
.venv\Scripts\activate.bat
```
```bash
# 3. Upgrade package manager internal venv
pip install --upgrade pip
```

### Install Depedensi
```bash
pip install -r requirements.txt
```

### Buat File requirements.txt
```bash
# requirements.txt

pyspark
pandas
numpy
scikit-learn
scipy
jupyter
```
