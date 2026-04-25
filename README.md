# 📊 Praktikum 3 — Batch Data Analytics + Visualization Layer
> **Big Data Dashboard | Microsoft Power BI / Business Intelligence**
> Program Studi Teknologi Informasi — UIN Antasari | Lecturer: Muhayat, M.IT

---

## 🛠️ Tech Stack

| Komponen | Detail |
|---|---|
| Programming Language | Python |
| Development Environment | Linux Server (WSL) |
| Code Editor | VS Code (Remote WSL) |
| Processing Engine | PySpark 4.1.1 |
| BI Platform | Power BI Desktop / Matplotlib |
| Durasi | 150 menit |

---

## 🎯 Tujuan Praktikum

1. Memahami peran **Visualization Layer** dalam arsitektur Big Data
2. Menggunakan **Power BI** untuk membuat dashboard analitik
3. Menghubungkan dataset hasil pipeline Spark ke tools BI
4. Membuat **KPI dashboard** sederhana dari dataset e-commerce
5. Menyajikan insight bisnis dari data yang telah diproses

---

## 🏗️ Arsitektur Pipeline

```
Raw Dataset (CSV)
       ↓
Spark Processing
       ↓
Clean Data (Parquet)
       ↓
Analytics Layer
       ↓
Serving Layer (CSV)
       ↓
Power BI Dashboard
```

---

## 📁 Struktur Folder Project

```
bigdata-project/
├── data/
│   ├── clean/
│   │   └── parquet/          ← Output dari pipeline sebelumnya
│   └── serving/              ← Output Analytics Layer
│       ├── total_revenue/
│       ├── top_products/
│       ├── category_revenue/
│       └── avg_transaction/
├── reports/
│   └── category_revenue.png  ← Output Visualization Layer
├── scripts/
│   ├── batch_pipeline_enterprise.py
│   ├── analytics_layer.py    ← Dibuat di praktikum ini
│   └── visualization_layer.py← Dibuat di praktikum ini
└── README.md
```

---

## ⚙️ Setup & Instalasi

### 1. Aktifkan Virtual Environment
```bash
source venv/bin/activate
```

> Jika venv belum ada, buat dulu:
> ```bash
> sudo apt install python3-venv python3-pip -y
> python3 -m venv venv
> source venv/bin/activate
> ```

### 2. Install Dependencies
```bash
pip install pandas matplotlib pyspark
```

---

## 🚀 Cara Menjalankan

### Bagian A — Analytics Layer

```bash
python scripts/analytics_layer.py
```

**Output yang dihasilkan:**

| KPI | Lokasi |
|---|---|
| Total Revenue | `data/serving/total_revenue/` |
| Top 10 Products | `data/serving/top_products/` |
| Revenue per Category | `data/serving/category_revenue/` |
| Avg Transaction Value | `data/serving/avg_transaction/` |

**Indikator berhasil:**
```
========================================
   ANALYTICS LAYER COMPLETED SUCCESS
   Execution Time: XX.XX sec
========================================
```

---

### Bagian B — Visualization Layer

#### Opsi 1: Matplotlib (Lokal)

```bash
# Buat folder reports terlebih dahulu
mkdir -p reports

python scripts/visualization_layer.py
```

Output: `reports/category_revenue.png`

Buka hasil visualisasi:
```bash
explorer.exe reports
```

#### Opsi 2: Power BI Desktop

1. Install Power BI: https://powerbi.microsoft.com/desktop
2. Buka Power BI Desktop
3. Import dataset:
   - `Home → Get Data → Text/CSV`
   - Pilih file dari folder `data/serving/`
4. Buat visualisasi:
   - **KPI Card** → drag field `total_revenue`
   - **Clustered Bar Chart** → Top Products (`product` vs `total_quantity`)
   - **Clustered Bar Chart** → Revenue per Category (`category` vs `category_revenue`)
5. Tambahkan judul: `E-Commerce Sales Dashboard`
6. Simpan: `File → Save → bigdata_dashboard.pbix`

---

## 📋 Checklist Validasi

| No | Validasi | Status |
|---|---|---|
| 1 | Analytics layer berhasil dijalankan | ✅ |
| 2 | Folder `data/serving` terbentuk | ✅ |
| 3 | Dataset berhasil diimport ke Power BI | ✅ |
| 4 | KPI Total Revenue tampil | ✅ |
| 5 | Top Product chart muncul | ✅ |
| 6 | Revenue per Category chart muncul | ✅ |
| 7 | Dashboard memiliki judul | ✅ |

---

## 📦 Output Wajib Dikumpulkan

- [ ] Screenshot dashboard Power BI
- [ ] File `bigdata_dashboard.pbix`
- [ ] Screenshot folder `data/serving`
- [ ] Screenshot terminal saat menjalankan `analytics_layer.py`

---

## ⚠️ Troubleshooting

### Virtual environment gagal dibuat
```bash
sudo apt install python3-venv python3-pip -y
python3 -m venv venv
```

### FileNotFoundError saat savefig
```bash
mkdir -p reports
```
Atau tambahkan `os.makedirs("reports", exist_ok=True)` di awal script.

### WARNING: NativeCodeLoader / hostname loopback
Warning ini **aman diabaikan** untuk penggunaan lokal/development. Tidak mempengaruhi hasil pipeline.

---

## 💡 Insight

> Power BI **tidak memproses** Big Data — ia hanya **menampilkan** hasil analisis.
> Proses utama terjadi di **Spark Processing Layer**.
> Visualization Layer hanya menyajikan KPI, Ranking, dan Kategori Revenue
> untuk mendukung pengambilan keputusan bisnis.

---

## 📊 Rubrik Penilaian

| Aspek | Skor 1 | Skor 2 | Skor 3 | Skor 4 |
|---|---|---|---|---|
| Menjalankan pipeline | Gagal | Sebagian | Berhasil | Sangat lancar |
| Import dataset | Tidak berhasil | Sebagian | Berhasil | Optimal |
| KPI visualization | Tidak ada | Kurang jelas | Baik | Sangat jelas |
| Chart analytics | Tidak ada | Sebagian | Lengkap | Sangat informatif |
| Layout dashboard | Berantakan | Kurang rapi | Rapi | Profesional |