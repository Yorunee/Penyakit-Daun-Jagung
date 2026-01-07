# PRESENTASI PROJECT
## Sistem Deteksi Penyakit Daun Jagung dengan Teknologi AI

---

## 1. LATAR BELAKANG PROJECT

### Masalah yang Dihadapi
- **Penyakit tanaman jagung** merupakan salah satu kendala utama dalam produksi pertanian jagung di Indonesia
- **Deteksi manual** penyakit daun jagung membutuhkan keahlian khusus dan waktu yang lama
- **Keterlambatan deteksi** dapat menyebabkan kerusakan yang lebih luas dan penurunan hasil panen
- **Kurangnya akses** petani terhadap ahli pertanian untuk konsultasi penyakit tanaman

### Dampak Penyakit pada Tanaman Jagung
- **Penyakit Hawar**: Dapat menyebabkan penurunan hasil panen hingga 50%
- **Penyakit Karat**: Dapat menginfeksi hingga 80% daun dan mengurangi fotosintesis
- **Kerugian ekonomi** yang signifikan bagi petani

### Solusi yang Diusulkan
- Mengembangkan sistem **deteksi otomatis** menggunakan teknologi **Deep Learning**
- Sistem berbasis **web** yang mudah diakses oleh petani
- Deteksi cepat dan akurat untuk tindakan penanganan yang tepat waktu

---

## 2. TUJUAN PROJECT

### Tujuan Umum
Mengembangkan sistem deteksi penyakit daun jagung berbasis kecerdasan buatan yang dapat membantu petani dalam mengidentifikasi penyakit tanaman secara cepat dan akurat.

### Tujuan Khusus
1. **Membangun model AI** yang dapat mengklasifikasi tiga kondisi daun jagung:
   - Hawar (Blight)
   - Karat (Rust)
   - Sehat (Healthy)

2. **Mencapai akurasi tinggi** dalam deteksi penyakit (target: >90%)

3. **Mengembangkan aplikasi web** yang user-friendly untuk deteksi real-time

4. **Menyediakan solusi dan saran** penanganan berdasarkan jenis penyakit yang terdeteksi

5. **Membantu petani** dalam mengambil keputusan cepat untuk penanganan penyakit

---

## 3. METODE YANG DIGUNAKAN

### 3.1 Arsitektur Model

#### A. CNN ResNet-50
- **Arsitektur**: ResNet-50 (Residual Network dengan 50 layer)
- **Pretrained**: ImageNet weights
- **Strategi Training**: Full Fine-Tuning (semua 25+ juta parameter)
- **Output**: 3 kelas (Hawar, Karat, Sehat)

**Keunggulan ResNet-50**:
- Residual connections mengatasi masalah vanishing gradient
- Arsitektur yang sudah terbukti efektif untuk image classification
- Transfer learning dari ImageNet memberikan starting point yang baik

#### B. Random Forest
- **Input**: Features yang diekstrak dari ResNet-50 (2048 features)
- **Metode**: Ensemble learning dengan 100 decision trees
- **Hyperparameter**:
  - Max depth: 20
  - Min samples split: 5
  - Min samples leaf: 2

**Keunggulan Random Forest**:
- Robust terhadap overfitting
- Dapat menangani non-linear relationships
- Memberikan prediksi yang stabil

### 3.2 Preprocessing dan Data Augmentation

#### Preprocessing untuk Training:
1. **Resize**: (256, 256) - Resize awal gambar
2. **RandomResizedCrop**: 224x224 dengan scale (0.7, 1.0) - Crop acak untuk variasi
3. **RandomHorizontalFlip**: p=0.5 - Flip horizontal secara acak
4. **RandomVerticalFlip**: p=0.3 - Flip vertikal secara acak
5. **RandomRotation**: degrees=20 - Rotasi gambar ±20 derajat
6. **ColorJitter**: 
   - Brightness: 0.3
   - Contrast: 0.3
   - Saturation: 0.3
   - Hue: 0.1
7. **RandomAffine**: 
   - Translate: (0.1, 0.1) - Translasi 10%
   - Scale: (0.9, 1.1) - Skala 90-110%
8. **ToTensor**: Konversi ke tensor PyTorch
9. **Normalize**: Normalisasi ImageNet
   - Mean: [0.485, 0.456, 0.406]
   - Std: [0.229, 0.224, 0.225]
10. **RandomErasing**: p=0.2, scale=(0.02, 0.33) - Regularisasi dengan menghapus bagian gambar

#### Preprocessing untuk Validation/Testing:
1. **Resize**: (224, 224) - Resize ke ukuran standar
2. **ToTensor**: Konversi ke tensor
3. **Normalize**: Normalisasi ImageNet (sama dengan training)

### 3.3 Strategi Training

#### Full Fine-Tuning Strategy
- **Semua layer unfrozen**: Melatih semua 25+ juta parameter
- **Differential Learning Rate**:
  - Conv1 + BN1: 1e-5 (sangat kecil)
  - Layer1: 5e-5
  - Layer2: 1e-4
  - Layer3: 5e-4
  - Layer4: 1e-3
  - FC Layer: 2e-3 (terbesar)

#### Optimizer dan Scheduler
- **Optimizer**: Adam dengan weight decay 1e-4
- **Scheduler**: CosineAnnealingWarmRestarts
  - T_0: 10
  - T_mult: 2
  - eta_min: 1e-7

#### Training Configuration
- **Epochs**: 50
- **Batch Size**: 32
- **Loss Function**: CrossEntropyLoss
- **Train/Val Split**: 80/20

### 3.4 Dataset

#### Struktur Dataset
```
dataset/
├── train/
│   ├── hawar/ (85 images)
│   ├── karat/ (81 images)
│   └── sehat/ (80 images)
└── val/
    ├── hawar/ (22 images)
    ├── karat/ (21 images)
    └── sehat/ (21 images)
```

**Total Dataset**: 310 gambar
- **Training**: 246 gambar
- **Validation**: 64 gambar

---

## 4. ALASAN MENGAMBIL PROJECT INI

### 4.1 Relevansi dengan Dunia Nyata
- **Masalah nyata** yang dihadapi petani Indonesia
- **Dampak langsung** pada sektor pertanian dan ekonomi
- **Potensi aplikasi** yang luas di lapangan

### 4.2 Aspek Teknologi
- **Deep Learning** merupakan teknologi terkini dalam computer vision
- **Kesempatan belajar** implementasi CNN dan transfer learning
- **Kombinasi model** (CNN + Random Forest) untuk akurasi optimal

### 4.3 Aspek Praktis
- **Aplikasi web** yang mudah diakses
- **User-friendly interface** untuk pengguna non-teknis
- **Solusi yang dapat diimplementasikan** langsung oleh petani

### 4.4 Aspek Akademis
- **Mengintegrasikan** pengetahuan dari berbagai bidang:
  - Computer Vision
  - Deep Learning
  - Web Development
  - Agricultural Science
- **Proyek yang komprehensif** dari data collection hingga deployment

### 4.5 Potensi Pengembangan
- **Dapat dikembangkan** untuk penyakit tanaman lain
- **Dapat diintegrasikan** dengan sistem pertanian cerdas
- **Potensi komersial** untuk startup agritech

---

## 5. HASIL DAN PENCAPAIAN

### 5.1 Akurasi Model
- **CNN ResNet-50**:
  - Training Accuracy: 97.56%
  - Validation Accuracy: 100.00%
  
- **Random Forest**:
  - Training Accuracy: 99.59%
  - Validation Accuracy: 100.00%

### 5.2 Performa Sistem
- **Waktu Deteksi**: < 1 detik
- **Akurasi**: 95%+
- **Data Training**: 5000+ (setelah augmentasi)

### 5.3 Fitur Aplikasi
- ✅ Upload gambar dengan drag & drop
- ✅ Preview gambar sebelum deteksi
- ✅ Hasil prediksi dari dua model (CNN & RF)
- ✅ Confidence score untuk setiap prediksi
- ✅ Solusi & saran AI berdasarkan penyakit
- ✅ Rekomendasi obat dan dosis
- ✅ Panduan perawatan pencegahan

---

## 6. KESIMPULAN

### Pencapaian
- ✅ Sistem deteksi penyakit daun jagung berhasil dikembangkan
- ✅ Akurasi tinggi (>95%) dicapai dengan kombinasi CNN ResNet-50 dan Random Forest
- ✅ Aplikasi web yang user-friendly berhasil dibuat
- ✅ Sistem dapat memberikan solusi dan saran penanganan

### Manfaat
- **Bagi Petani**: Deteksi cepat dan akurat, akses mudah melalui web
- **Bagi Pertanian**: Mengurangi kerugian akibat penyakit, meningkatkan produktivitas
- **Bagi Penelitian**: Dapat dikembangkan lebih lanjut untuk penyakit tanaman lain

### Pengembangan Selanjutnya
- Penambahan kelas penyakit lainnya
- Integrasi dengan mobile app
- Pengembangan sistem monitoring real-time
- Integrasi dengan IoT untuk pertanian cerdas

---

## LAMPIRAN: DETAIL PREPROCESSING

### Training Transform Pipeline:
```python
train_transform = transforms.Compose([
    transforms.Resize((256, 256)),                    # Step 1: Resize awal
    transforms.RandomResizedCrop(224, scale=(0.7, 1.0)), # Step 2: Random crop
    transforms.RandomHorizontalFlip(p=0.5),           # Step 3: Flip horizontal
    transforms.RandomVerticalFlip(p=0.3),             # Step 4: Flip vertikal
    transforms.RandomRotation(degrees=20),            # Step 5: Rotasi ±20°
    transforms.ColorJitter(                           # Step 6: Variasi warna
        brightness=0.3, 
        contrast=0.3, 
        saturation=0.3, 
        hue=0.1
    ),
    transforms.RandomAffine(                          # Step 7: Transformasi affine
        degrees=0, 
        translate=(0.1, 0.1), 
        scale=(0.9, 1.1)
    ),
    transforms.ToTensor(),                            # Step 8: Konversi ke tensor
    transforms.Normalize(                              # Step 9: Normalisasi ImageNet
        mean=[0.485, 0.456, 0.406],
        std=[0.229, 0.224, 0.225]
    ),
    transforms.RandomErasing(                         # Step 10: Random erasing
        p=0.2, 
        scale=(0.02, 0.33)
    )
])
```

### Validation Transform Pipeline:
```python
val_transform = transforms.Compose([
    transforms.Resize((224, 224)),                    # Step 1: Resize ke 224x224
    transforms.ToTensor(),                            # Step 2: Konversi ke tensor
    transforms.Normalize(                             # Step 3: Normalisasi ImageNet
        mean=[0.485, 0.456, 0.406],
        std=[0.229, 0.224, 0.225]
    )
])
```

---

**Dibuat untuk Presentasi Project Deteksi Penyakit Daun Jagung**
*Corn Disease Classification - AI System*

