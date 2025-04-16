# 🔧 DS Series: Prediksi dan Estimasi Perbaikan Mesin Industri

![Python](https://img.shields.io/badge/Python-3.9-blue?logo=python)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-development-yellow)
![Made with Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?logo=Jupyter)

📅 **Tanggal**: April 16, 2025  
👨‍💻 **Author**: Alan Firdaus  
📦 **Episode**: 1 dari Portofolio Data Science Series

---

## 🎯 Tujuan Proyek

Proyek ini bertujuan untuk:
- Memprediksi **kerusakan mesin industri** berdasarkan **jam operasi**.
- Menyediakan **estimasi sisa umur mesin** serta waktu optimal untuk **perbaikan atau penggantian suku cadang**.
- Menggunakan pendekatan **unsupervised learning** karena tidak tersedia label kerusakan.

---

## 📊 Dataset

Dataset yang digunakan terdiri dari **1200 baris** dan 6 fitur utama:

| Fitur             | Deskripsi                               |
|------------------|-----------------------------------------|
| `Jam_Operasi`     | Total jam mesin telah beroperasi       |
| `Suhu_Motor`      | Suhu rata-rata motor selama beroperasi |
| `Getaran`         | Tingkat getaran mesin                   |
| `Tekanan_Oli`     | Tekanan oli dalam sistem                |
| `Arus_Listrik`    | Beban listrik yang digunakan            |
| `Umur_Sisa_Mesin` | Estimasi sisa umur mesin (label dummy)  |

---

## 🔎 Tahapan Analisis

### 1. Data Wrangling
- Mengecek missing value dan duplikasi (✅ Tidak ada)
- Deteksi outlier dengan **Boxplot + IQR**
- Bersihkan data menggunakan **IQR** dan **Winsorize**

### 2. Exploratory Data Analysis (EDA)
- Visualisasi distribusi fitur menggunakan **Histogram, KDE, PDF, ECDF**
- Uji normalitas dengan **Shapiro-Wilk Test**
- Insight penting:
  - Hanya sebagian kecil fitur memiliki distribusi normal
  - Tidak ada korelasi kuat antara fitur terhadap umur mesin → hindari regresi linier

### 3. Analisis Korelasi & Pengaruh Suhu
- Korelasi Spearman → Semua fitur lemah terhadap `Umur_Sisa_Mesin`
- Grup suhu menunjukkan tren getaran dan tekanan oli → digunakan untuk membuat **Label Pemeliharaan**

---

## 🧠 Feature Engineering

- **Skoring Pemeliharaan Mesin**:
  - Normalisasi anomaly score → range 0–100
  - Hitung degradasi antar waktu (`diff`) dan rolling average
  - Identifikasi **penurunan tajam** sebagai titik kritis

- **Label Kategori Suhu** (Normal, Perlu Dicek, Ganti Sparepart)

---

## 🧪 Modeling

### 🔍 PCA (Principal Component Analysis)
- Reduksi fitur → 2 komponen: `PC1`, `PC2`

### 🌲 Isolation Forest
- Mendeteksi anomali tanpa label
- Hasil:
  - ~21% data diklasifikasikan sebagai **anomali**
  - Silhouette Score: **0.1387** (struktur cluster cukup lemah)

### 💡 Visualisasi:
- **Scatterplot PCA + Label Anomali**
- **Line Plot Skor Umur vs Jam Operasi**
- **Heatmap Skor Mesin per Interval Waktu**

---

## 📈 Analisis Lanjutan

### 🔥 Deteksi Titik Kritis
- Penurunan > 5 poin dianggap **signifikan**
- Dibagi ke dalam:
  - **Ringan**: -5 s/d -10
  - **Sedang**: -10 s/d -20
  - **Berat**: < -20

### 🔄 Heatmap & Rolling Average
- Melacak skor sisa umur mesin secara waktu
- Menemukan jam operasi > 5000 sebagai fase rawan degradasi

---

## 🧩 Rencana Pengembangan Selanjutnya

- 🚀 Deploy ke Streamlit atau Flask
- 📊 Tambahkan dashboard interaktif untuk engineer
- 🔍 Uji model unsupervised lainnya seperti **LOF**
- ⚙️ Buat sistem notifikasi **early warning** berdasarkan degradasi

---

## 🙌 Penutup

Proyek ini merupakan bagian dari seri portofolio Data Science saya, dengan fokus pada **analisis perawatan mesin industri** berbasis data. Pendekatan ini diharapkan bisa membantu perusahaan dalam **mengoptimalkan produksi** dan **mengurangi downtime akibat kerusakan mesin**.

> 📧 Untuk kolaborasi dan diskusi: firdauslan13@gmail.com

