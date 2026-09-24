# Tugas Density Based Clustering dengan DBSCAN

## Identitas Mahasiswa

* Nama : Muhammad Gauza Faliha
* Kelas : KOM A
* NIM : 25/555851/PA/23315
* Program Studi : Ilmu Komputer
* Fakultas : Matematika dan Ilmu Pengetahuan Alam
* Universitas : Universitas Gadjah Mada


## Arsitektur Singkat dan Alur Kerja

Arsitektur solusi dalam tugas ini dibangun melalui 6 tahapan komputasi utama:

1. **Eksplorasi Data Statistik**:
   Pemeriksaan ringkasan statistik (minimum, maksimum, mean, median, standar deviasi, dan skewness) pada enam fitur pengeluaran tahunan: Fresh, Milk, Grocery, Frozen, Detergents_Paper, dan Delicassen. Tahapan ini memperlihatkan sifat data yang memiliki rentang sangat luas, variabilitas tinggi, serta kemencengan positif ekstrem (heavy right tail).

2. **Preprocessing Data**:
   * Transformasi Logaritma Natural `ln(1 + x)` menggunakan fungsi `np.log1p` untuk memampatkan sebaran skala multiplikatif dan mereduksi derajat kemencengan ekstrem mendekati nol.
   * Standardisasi Z Score menggunakan `StandardScaler` agar seluruh fitur memiliki nilai rata rata 0 dan variansi 1, mencegah dominasi fitur berskala besar dalam metrik jarak Euclidean.

3. **Penentuan Parameter Kepadatan melalui Grafik K Distance**:
   Perhitungan jarak Euclidean ke tetangga terdekat ke 6 (k = min samples = 6 sesuai dimensi data D = 6). Kurva k distance yang diurutkan menaik dianalisis untuk mendeteksi titik siku lutut (knee point) pada rentang eps 1.2 hingga 1.5 sebagai pemisah area padat dan kawasan renggang.

4. **Implementasi DBSCAN (From Scratch)**:
   Membangun kelas `DBSCANFromScratch` berbasis matriks NumPy murni. Algoritma menghitung matriks jarak berpasangan, mengidentifikasi titik inti (core points), melakukan penelusuran antrean BFS untuk menghubungkan titik density reachable dan density connected, menandai titik perbatasan (border points), serta menetapkan titik terisolasi sebagai titik bising noise (label minus satu).

5. **Analisis Profil Bisnis dan Deteksi Anomali**:
   Perhitungan nilai rata rata pengeluaran produk asli pada klaster reguler (Klaster 0) dan titik bising noise. Mengidentifikasi pelanggan skala menengah berimbang (Klaster 0) serta pelanggan raksasa dengan pola belanja ekstrem (titik noise seperti indeks 181, 65, dan 23).

6. **Perbandingan Komparatif dengan KMeans**:
   Membandingkan hasil DBSCAN dengan algoritma partisional KMeans (k = 2) dalam hal keseimbangan ukuran anggota, interpretabilitas bisnis terhadap kanal Horeca dan Retail, serta evaluasi kesesuaian algoritma pada dataset Wholesale Customers.



## Panduan Instalasi dan Penggunaan

Ikuti langkah langkah berikut untuk menyiapkan lingkungan kerja dan menjalankan notebook:

### 1. Kloning atau Buka Direktori Proyek

Buka terminal PowerShell atau Command Prompt pada folder proyek ini:

```bash
cd "d:\10. KULIAH COMPSCIE SEMESTER 3\AI\Tugas DBSCAN"
```

### 2. Membuat dan Mengaktifkan Lingkungan Virtual

Disarankan menggunakan lingkungan virtual Python agar pustaka terisolasi secara rapi:

Untuk pengguna Windows PowerShell:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Untuk pengguna Command Prompt:
```cmd
python -m venv .venv
.\.venv\Scripts\activate.bat
```

### 3. Instalasi Library 

Pasang seluruh pustaka yang diperlukan menggunakan perintah pip berikut:

```bash
pip install ucimlrepo scikit_learn pandas numpy matplotlib
```

Daftar pustaka utama:
* `numpy` : Komputasi numerik dan operasi matriks from scratch
* `pandas` : Manipulasi data dan tabulasi statistik
* `matplotlib` : Pembuatan visualisasi grafik distribusi dan ruang PCA
* `scikit_learn` : Pustaka pembantu untuk StandardScaler, PCA, KMeans, dan metrik evaluasi
* `ucimlrepo` : Pengambilan data otomatis dari UCI Machine Learning Repository

### 4. Menjalankan Jupyter Notebook

Jalankan server notebook lokal melalui perintah:

```bash
jupyter notebook
```

Buka berkas `Tugas_Density_Based_Clustering_dengan_DBSCAN.ipynb` lalu jalankan seluruh sel secara berurutan dari atas ke bawah.


