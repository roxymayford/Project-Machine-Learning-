# Tugas Bagian A: Dasar Data dan Pemahaman Granularitas

**Studi Kasus:** *Customer Behavior & Retail Transaction Analysis*  
**Dataset:** `customer_behavior_phase1.csv` (10.000 baris transaksi sepanjang tahun 2026, 19 kolom variabel)  
**Cakupan:** **Bagian A** meliputi Klasifikasi Variabel (A.1), Audit Kualitas Data (A.2), dan Analisis Tingkat Pelanggan vs. Tingkat Transaksi (A.3).

***

## Deskripsi Kolom Dataset

| Nama Kolom | Tipe Data | Keterangan |
|---|---|---|
| `Transaction_ID` | Kategorikal (ID) | Kode unik untuk setiap transaksi (TRX-000001 s.d. TRX-010000) |
| `Customer_ID` | Kategorikal (ID) | Kode unik pelanggan (satu pelanggan dapat bertransaksi lebih dari satu kali) |
| `Age` | Numerik (Diskrit) | Usia pelanggan dalam tahun (rentang 18 s.d. 65 tahun) |
| `Gender` | Kategorikal (Nominal) | Jenis kelamin pelanggan (Male, Female) |
| `City` | Kategorikal (Nominal) | Kota domisili pelanggan |
| `Region` | Kategorikal (Nominal) | Wilayah geografis utama (Jabodetabek, West Java, Central Java, East Java, Sumatera) |
| `Membership_Level` | Kategorikal (Ordinal) | Tingkatan keanggotaan pelanggan (Basic, Silver, Gold, Premium) |
| `Product_Category` | Kategorikal (Nominal) | Kategori produk yang dibeli (5 kategori utama) |
| `Product_Name` | Kategorikal (Nominal) | Nama spesifik produk yang dibeli |
| `Quantity` | Numerik (Diskrit) | Jumlah unit produk yang dibeli dalam satu transaksi |
| `Unit_Price` | Numerik (Kontinu) | Harga satuan produk sebelum diskon (dalam Rupiah) |
| `Discount_Percentage` | Numerik (Kontinu) | Persentase potongan harga yang diberikan (0% s.d. 50%) |
| `Purchase_Amount` | Numerik (Kontinu) | Total nilai pembayaran bersih setelah diskon (dalam Rupiah) |
| `Payment_Method` | Kategorikal (Nominal) | Metode pembayaran yang digunakan saat transaksi |
| `Store_Type` | Kategorikal (Nominal) | Kanal atau tipe toko tempat transaksi terjadi |
| `Purchase_Date` | Temporal (Tanggal) | Tanggal terjadinya transaksi sepanjang tahun 2026 (YYYY-MM-DD) |
| `Purchase_Hour` | Numerik (Diskrit) | Jam terjadinya transaksi dalam format 24 jam (0 s.d. 23) |
| `Purchase_Day` | Kategorikal (Ordinal) | Nama hari transaksi (Monday s.d. Sunday) |
| `Customer_Satisfaction` | Numerik / Ordinal | Skor kepuasan pelanggan setelah bertransaksi (skala 1 s.d. 5) |

***

## Struktur File Repositori

| File | Deskripsi |
|---|---|
| `customer_behavior_phase1.csv` | Dataset asli transaksi ritel omnichannel tahun 2026 (10.000 baris × 19 kolom). |
| `TugasBagianA_Kelompok.xlsx` | **File 1 (Pengelompokan Kategori dan Analisis A.3):** Workbook Excel dengan 10 sheet dan rumus aktif berisi `Raw_Data`, `A1_Klasifikasi`, 6 sheet pengelompokan tipe data (`Identifier`, `Nominal`, `Ordinal`, `Diskrit`, `Kontinu`, `Temporal`), `A3_Analisis_Deskriptif` (dilengkapi tabel bin, 2 histogram usia, dan grafik gender), serta `A3_Pelanggan_Unik`. |
| `TugasBagianA_Bersih.xlsx` | **File 2 (Dataset Bersih):** Workbook Excel dengan 3 sheet (`Data_Bersih`, `Log_Pembersihan`, `Data_Dikeluarkan`) berisi **9.557 baris** data yang sudah distandardisasi tipe datanya serta bersih dari anomali operasional gerai fisik (transaksi `Cash` pada kanal daring tetap dipertahankan sebagai COD). |
| `TugasBagianA.ipynb` | Jupyter Notebook Python (seluruh sel sudah dieksekusi) berisi pembuktian kuantitatif Bagian A.2 (`isnull().sum()`, `duplicated().sum()`, konsistensi matematis, tipe data, dan anomali operasional) serta verifikasi A.1 dan A.3 menggunakan `seaborn` dan `matplotlib`. |
| `TugasBagianB.ipynb` | Jupyter Notebook Python berisi analisis Bagian B (statistik deskriptif dan evaluasi outlier metode IQR). |
| `TugasBagianC.ipynb` | Jupyter Notebook Python berisi analisis Bagian C (visualisasi data untuk empat hipotesis bisnis dan rekomendasi strategis). |
| `RaihanGraniaSatya_TugasAkhir_Fase1.ipynb` | **Notebook Gabungan A, B, dan C (sesuai brief tugas, seluruh sel sudah dieksekusi):** menggabungkan Bagian A (dataset mentah `10.000` baris), Bagian B, dan Bagian C dengan basis data utama yang diselaraskan (`Data_Bersih` `9.557` baris, diskon `0% s.d. 50%`), penanda `148` transaksi mencurigakan sesuai keputusan outlier B.3.4, uji ketahanan Bagian C, serta narasi insight lengkap di bawah setiap grafik. |
| `RaihanGraniaSatya_TugasAkhir_Fase1.pdf` | **Laporan Analisis Utama (PDF):** dokumen laporan akhir terstruktur untuk Bagian A, B, dan C lengkap dengan tabel ringkasan statistik, grafik beresolusi tinggi, dan rekomendasi bisnis. |
| `charts/` | Folder keluaran grafik beresolusi tinggi (300 DPI) untuk seluruh visualisasi Bagian A, B, dan C. |
| `README.md` | Dokumentasi deskripsi dataset, identifikasi bagian data bermasalah, dan hasil analisis Tugas Bagian A. |

***

## Hasil Analisis Bagian A

### A.1: Klasifikasi Variabel Statistik (19 Kolom)

Pengelompokan 19 kolom pada `TugasBagianA_Kelompok.xlsx` sesuai **Deskripsi Kolom Dataset**:

| Kelompok Tipe Data | Jumlah Kolom | Proporsi | Sheet Excel | Daftar Kolom |
|---|---:|---:|---|---|
| **Identifier** | 2 | 10,5% | `Identifier` | `Transaction_ID`, `Customer_ID` |
| **Nominal** | 7 | 36,8% | `Nominal` | `Gender`, `City`, `Region`, `Product_Category`, `Product_Name`, `Payment_Method`, `Store_Type` |
| **Ordinal** | 3 | 15,8% | `Ordinal` | `Membership_Level`, `Purchase_Day`, `Customer_Satisfaction` |
| **Diskrit** | 3 | 15,8% | `Diskrit` | `Age`, `Quantity`, `Purchase_Hour` |
| **Kontinu** | 3 | 15,8% | `Kontinu` | `Unit_Price`, `Discount_Percentage`, `Purchase_Amount` |
| **Temporal** | 1 | 5,3% | `Temporal` | `Purchase_Date` |
| **Total** | **19** | **100,0%** | **6 Sheet** | **19 kolom terklasifikasi** |

#### Penjelasan Khusus: `Customer_Satisfaction` dan `Purchase_Hour`
1. **`Customer_Satisfaction` (Kategorikal Ordinal):**  
   Meskipun tersimpan sebagai angka bulat `1` hingga `5`, nilai ini merupakan skala Likert yang menyatakan tingkatan/peringkat persepsi kepuasan (`1 = Sangat Tidak Puas` hingga `5 = Sangat Puas`). Jarak psikologis antar skor tidak dijamin seragam dan tidak memiliki titik nol absolut, sehingga klasifikasi statistiknya adalah **Ordinal**.
2. **`Purchase_Hour` (Numerik Diskrit):**  
   Sesuai deskripsi dataset, `Purchase_Hour` diklasifikasikan sebagai **Numerik Diskrit** karena nilainya berupa bilangan bulat terbatas dalam format 24 jam (`0` s.d. `23`, tanpa pecahan). Sebagai catatan, variabel jam memiliki sifat siklis (jam `23` berdekatan dengan jam `0`), sehingga analisis distribusi per jam dan jam puncak (modus) lebih informatif dibandingkan rata rata linear semata.

***

### A.2: Audit Kualitas Data dan Identifikasi Bagian Data yang Bermasalah (`TugasBagianA.ipynb`)

#### 1. Pengecekan Dasar Kualitas Data (Missing Value, Duplikat, Matematis, Relasional)

| No | Dimensi Audit | Metode di Notebook | Hasil | Status |
|---:|---|---|---|---|
| 1 | **Missing Value (`NaN` / `Null`)** | `df.isnull().sum()` dan `df.isnull().sum().sum()` | `0` missing value pada seluruh 19 kolom (`100%` terisi) | **BERSIH** |
| 2 | **String / Spasi Kosong** | Pengecekan `.str.strip() == ''` pada semua kolom teks | `0` temuan | **BERSIH** |
| 3 | **Baris Duplikat Identik** | `df.duplicated().sum()` | `0` baris duplikat | **BERSIH** |
| 4 | **Duplikasi `Transaction_ID`** | `df['Transaction_ID'].duplicated().sum()` | `0` duplikat (`10.000` ID unik) | **BERSIH** |
| 5 | **Duplikasi Transaksi (Tanpa ID)** | `df.duplicated(subset=kolom_non_id).sum()` | `0` baris | **BERSIH** |
| 6 | **Konsistensi Matematis `Purchase_Amount`** | `Quantity × Unit_Price × (1 - Discount%/100)` | `0` baris tidak konsisten (selisih maks `Rp 0,00`) | **100% KONSISTEN** |
| 7 | **Konsistensi `Purchase_Date` dan `Purchase_Day`** | `pd.to_datetime()` dan pencocokan `day_name()` | `0` tanggal invalid dan `0` mismatch hari | **BERSIH** |
| 8 | **Relasi `City` ke `Region` dan `Product_Name` ke `Product_Category`** | Pengecekan pemetaan 1 ke 1 | `0` konflik pemetaan | **BERSIH** |
| 9 | **Konsistensi Profil per `Customer_ID`** | Pengecekan `Age`, `Gender`, `City`, `Region`, `Membership_Level` | `0` pelanggan dengan atribut berubah ubah | **BERSIH** |

> Pengulangan `Customer_ID` pada 7.124 dari 10.000 baris bukan duplikasi error, melainkan transaksi berulang (*repeat purchase*) yang sah dari **2.876 pelanggan unik**. Selain itu, **349 transaksi `Cash` pada kanal daring** (`Online App`: 278 baris; `Official Web`: 71 baris) tetap **dipertahankan** karena valid sebagai transaksi **COD (*Cash on Delivery*)**.

#### 2. Temuan Bagian Data yang Bermasalah / Tidak Sesuai (Tipe Data dan Anomali Operasional)

Audit mendalam pada `customer_behavior_phase1.csv` mengidentifikasi **4 titik permasalahan tipe data dan logika operasional**:

| No | Bagian / Kolom Bermasalah | Temuan Spesifik | Jumlah Baris | Contoh di Dataset | Penanganan di `TugasBagianA_Bersih.xlsx` |
|---:|---|---|---:|---|---|
| 1 | **Tipe Data Kolom CSV** (`Purchase_Date`, `Unit_Price`, `Discount_Percentage`, `Purchase_Amount`) | `Purchase_Date` tersimpan sebagai teks (`string`/`object`), belum bertipe tanggal (`datetime`). Selain itu, `Unit_Price`, `Discount_Percentage`, dan `Purchase_Amount` tersimpan sebagai desimal `.0` (`float64`) padahal 100% nilainya bilangan bulat. | `10.000` baris (format) | `520000.0`, `0.0`, `"2026-01-01"` | Dikonversi menjadi tipe tanggal asli (`YYYY-MM-DD`), bilangan bulat Rupiah (`"Rp "#,##0`), dan persentase bersih (`0%`). |
| 2 | **`Store_Type` dan `Purchase_Hour`** | Transaksi pada gerai fisik (`Flagship Store`: **222 baris**, `Mall Outlet`: **215 baris**) tercatat di luar jam operasional normal mal/gerai, yakni pukul **`00:00` s.d. `07:00`** dan **`23:00`**. | **437 baris** | `TRX-000028` (`Flagship Store`, jam `07`), `TRX-000106` (`Flagship Store`, jam `05`), `TRX-000127` (`Flagship Store`, jam `02`) | Dikeluarkan dari `Data_Bersih` dan dicatat pada sheet `Data_Dikeluarkan`. |
| 3 | **`Customer_ID`, `Purchase_Date`, `Purchase_Hour`, dan `Store_Type`** | Satu `Customer_ID` tercatat bertransaksi pada **tanggal dan jam yang sama persis di 2 gerai fisik berbeda sekaligus (`Mall Outlet` dan `Flagship Store`)**. | **6 baris** (3 pasang) | `CUST-02243` (`2026-06-10` jam `20`: `TRX-004284` dan `TRX-004285`), `CUST-00679` (`2026-07-27` jam `15`: `TRX-005563` dan `TRX-005564`), `CUST-01950` (`2026-11-22` jam `11`: `TRX-008687` dan `TRX-008688`) | Dikeluarkan dari `Data_Bersih` dan dicatat pada sheet `Data_Dikeluarkan`. |
| 4 | **Rentang dan Batas Atas `Age`** | Deskripsi dataset menyatakan rentang `18` s.d. `65` tahun, namun usia minimum aktual adalah `19` tahun (0 data usia `18`) dan terjadi penumpukan tajam tepat di batas atas `Age = 65` (`100` transaksi / `28` pelanggan unik, dibanding `Age = 64` hanya `10` transaksi / `5` pelanggan yang mengindikasikan pemotongan/*capping* usia). | Catatan distribusi (`100` baris di usia `65`) | `Age = 64` (10 trx) vs `Age = 65` (100 trx) | Dipertahankan (usia `65` tetap valid dalam rentang `18` s.d. `65`) sebagai catatan distribusi. |

**Rekap Pembersihan pada `TugasBagianA_Bersih.xlsx`:**
1. Dataset awal: **`10.000` baris**
2. Total baris anomali operasional dikeluarkan (`437 + 6`, tanpa irisan): **`443` baris** (`4,43%`), tersimpan di sheet `Data_Dikeluarkan` lengkap dengan kolom `Alasan_Pembersihan`
3. Dataset bersih (`Data_Bersih`): **`9.557` baris** (`95,57%`), sudah terstandardisasi tipe datanya, bebas anomali gerai fisik, dan mempertahankan `349` transaksi `Cash` daring (COD).

***

### A.3: Analisis Tingkat Pelanggan vs. Tingkat Transaksi (`TugasBagianA_Kelompok.xlsx`)

#### 1. Ringkasan Granularitas
1. **Total Transaksi (Tingkat Transaksi):** `10.000` transaksi
2. **Total Pelanggan Unik (Tingkat Pelanggan):** `2.876` pelanggan unik (`Customer_ID`)
3. **Frekuensi Transaksi per Pelanggan:** Rata rata **`3,48`** transaksi | Median **`3,00`** | Rentang **`1` s.d. `137`** transaksi (`78,48%` merupakan *repeat buyer*).

#### 2. Perbandingan Statistik Deskriptif `Age`

| Statistik (`Age`) | Tingkat Transaksi (`n = 10.000`) | Pelanggan Unik (`n = 2.876`) | Selisih (Trx vs Unik) |
|---|---:|---:|---:|
| **Mean** | `36,9085` tahun | **`36,9555` tahun** | `-0,0470` tahun |
| **Standard Error** | `0,0885` | `0,1657` | `-0,0773` |
| **Median** | `35,00` tahun | **`36,00` tahun** | `-1,00` tahun |
| **Mode** | `32` tahun | **`35` tahun** | `-3` tahun |
| **Standard Deviation** | `8,8467` | `8,8886` | `-0,0418` |
| **Sample Variance** | `78,2648` | `79,0067` | `-0,7420` |
| **Kurtosis** | `0,4979` | `0,4031` | `+0,0948` |
| **Skewness** | `0,8414` | `0,7916` | `+0,0498` |
| **Minimum / Maximum** | `19` / `65` | `19` / `65` | `0` |
| **Q1 / Q3 / IQR** | `30` / `42` / `12` | `30` / `42` / `12` | `0` |

#### 3. Perbandingan Distribusi `Gender`

| Gender | Jumlah Transaksi | % Transaksi | Pelanggan Unik | % Pelanggan Unik | Selisih (%) | Avg Trx / Pelanggan |
|---|---:|---:|---:|---:|---:|---:|
| **Female** | `4.951` | `49,51%` | **`1.463`** | **`50,87%`** | `-1,36%` | `3,38` |
| **Male** | **`5.049`** | **`50,49%`** | `1.413` | `49,13%` | `+1,36%` | **`3,57`** |
| **Total** | **`10.000`** | **`100,00%`** | **`2.876`** | **`100,00%`** | `0,00%` | **`3,48`** |

#### 4. Penyebab Perbedaan dan Validitas Metrik
1. **Mengapa hasil berbeda?**  
   Karena **perbedaan granularitas dan pembobotan frekuensi transaksi (*repeat purchase bias*)**. Pada level transaksi, satu pelanggan dihitung berulang sesuai jumlah transaksinya. Misalnya `CUST-00679` (Male, 32 tahun) muncul **137 kali** dan `CUST-01469` (Male, 34 tahun) muncul **69 kali**. Akibatnya, rata rata usia turun tipis (`36,96` ke `36,91`), median turun (`36` ke `35`), modus bergeser dari `35` ke `32` tahun, dan **mayoritas Gender berbalik** dari **Female (`50,87%`)** pada pelanggan unik menjadi **Male (`50,49%`)** pada level transaksi karena rata rata frekuensi belanja Male (`3,57` trx/orang) lebih tinggi dari Female (`3,38` trx/orang).
2. **Metrik mana yang lebih valid?**  
   **Tingkat Pelanggan Unik (`n = 2.876`)** lebih valid untuk menggambarkan **profil demografi pelanggan**, karena setiap individu pelanggan memiliki bobot setara (dihitung tepat satu kali) sehingga bebas dari distorsi *repeat buyer*. Sementara itu, perhitungan tingkat transaksi lebih tepat untuk mengukur **kontribusi volume transaksi** tiap segmen demografi.
