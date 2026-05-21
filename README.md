# 📸 PENGOLAHAN CITRA DIGITAL — FEATURE MATCHING ORB

## 👩‍🎓 Identitas Mahasiswa

| Keterangan | Isi |
|---|---|
| 👤 Nama | **Muhamad valenino ramzi** |
| 🆔 NIM | **3124104544** |
| 🏫 Kelas | **I241E** |
| 📚 Mata Kuliah | **Pengolahan Citra** |
| 👨‍🏫 Dosen Pengampu | **Dr. Muhamad Fatchan, S.Kom., M.Kom.** |

---

# 📖 Deskripsi Tugas

Tugas ini bertujuan untuk memahami proses **Feature Matching** menggunakan algoritma **ORB (Oriented FAST and Rotated BRIEF)** pada Python dengan library OpenCV.

Algoritma ORB digunakan untuk:
- 🔍 mendeteksi titik penting pada gambar (*keypoints*)
- 📌 membuat descriptor
- 🔗 mencocokkan fitur antara dua gambar

Pada praktikum ini dilakukan proses:
1. Membaca gambar
2. Mengubah gambar menjadi grayscale
3. Mendeteksi keypoints menggunakan ORB
4. Melakukan feature matching menggunakan BFMatcher
5. Menampilkan hasil pencocokan fitur

---

# 🛠️ Library yang Digunakan

Berikut library yang digunakan pada program:

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt
```

## ✨ Penjelasan Library

### 📌 NumPy
Digunakan untuk operasi numerik dan array pada Python.

### 📌 OpenCV (cv2)
Digunakan untuk pengolahan citra digital seperti:
- membaca gambar
- grayscale
- ORB
- feature matching

### 📌 Matplotlib
Digunakan untuk menampilkan hasil gambar.

---

# 💻 Source Code Program

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt

query_img = cv2.imread('sports-car test.webp')
train_img = cv2.imread('sports-car train.webp')

query_img_bw = cv2.cvtColor(query_img, cv2.COLOR_BGR2GRAY)
train_img_bw = cv2.cvtColor(train_img, cv2.COLOR_BGR2GRAY)

orb = cv2.ORB_create()

queryKeypoints, queryDescriptors = orb.detectAndCompute(query_img_bw, None)
trainKeypoints, trainDescriptors = orb.detectAndCompute(train_img_bw, None)

matcher = cv2.BFMatcher()

matches = matcher.match(queryDescriptors, trainDescriptors)

final_img = cv2.drawMatches(
    query_img,
    queryKeypoints,
    train_img,
    trainKeypoints,
    matches[:20],
    None
)

final_img = cv2.resize(final_img, (1000, 650))

plt.figure(figsize=(10, 6))
plt.imshow(cv2.cvtColor(final_img, cv2.COLOR_BGR2RGB))
plt.title("Feature Matches")
plt.axis('off')

plt.show()
```

---

# 🧩 Penjelasan Program

## 📥 Membaca Gambar

```python
query_img = cv2.imread('sports-car test.webp')
train_img = cv2.imread('sports-car train.webp')
```

Kode di atas digunakan untuk membaca dua gambar:
- gambar query
- gambar train

Kedua gambar tersebut nantinya akan dibandingkan menggunakan algoritma ORB.

### 📸 Hasil Membaca Gambar

![Gambar Asli](https://github.com/ramzi121006/pengolahan_citra_ORB/blob/6b022779eb6a6b95345dca02b7ac256c9e181f69/Screenshot%202026-05-21%20141230.png)

---

# 🎨 Mengubah Gambar Menjadi Grayscale

```python
query_img_bw = cv2.cvtColor(query_img, cv2.COLOR_BGR2GRAY)
train_img_bw = cv2.cvtColor(train_img, cv2.COLOR_BGR2GRAY)
```

Proses grayscale dilakukan agar gambar menjadi abu-abu.

Tujuan grayscale:
- mempermudah proses deteksi fitur
- mengurangi kompleksitas warna
- mempercepat proses ORB

### 📸 Hasil Grayscale

![Grayscale](Screenshot_Hasil_ORB/SS_2_Grayscale.png)

---

# 🔍 Deteksi Keypoints Menggunakan ORB

```python
orb = cv2.ORB_create()
```

Kode tersebut digunakan untuk membuat objek ORB.

---

## 📌 Mendeteksi Keypoints dan Descriptor

```python
queryKeypoints, queryDescriptors = orb.detectAndCompute(query_img_bw, None)
trainKeypoints, trainDescriptors = orb.detectAndCompute(train_img_bw, None)
```

Fungsi:
- mendeteksi titik penting pada gambar
- membuat descriptor dari setiap keypoint

### ✨ Keypoints
Merupakan titik unik pada gambar seperti:
- sudut
- tekstur
- pola tertentu

### ✨ Descriptor
Merupakan data numerik yang digunakan untuk membandingkan fitur antar gambar.

### 📸 Hasil Keypoints ORB

![Keypoints ORB](Screenshot_Hasil_ORB/SS_3_Keypoints_ORB.png)

---

# 🔗 Feature Matching Menggunakan BFMatcher

```python
matcher = cv2.BFMatcher()
```

BFMatcher (*Brute Force Matcher*) digunakan untuk mencocokkan descriptor antara dua gambar.

---

## 📌 Melakukan Pencocokan Fitur

```python
matches = matcher.match(queryDescriptors, trainDescriptors)
```

Kode tersebut digunakan untuk:
- membandingkan descriptor
- mencari pasangan fitur yang paling mirip

---

# 🖼️ Menampilkan Hasil Feature Matching

```python
final_img = cv2.drawMatches(
    query_img,
    queryKeypoints,
    train_img,
    trainKeypoints,
    matches[:20],
    None
)
```

Kode tersebut digunakan untuk:
- menggambar hasil pencocokan fitur
- menampilkan garis penghubung antar keypoints

---

# 📏 Resize Gambar

```python
final_img = cv2.resize(final_img, (1000, 650))
```

Digunakan untuk memperbesar tampilan hasil agar lebih jelas dilihat.

---

# 📊 Menampilkan Output

```python
plt.figure(figsize=(10, 6))
plt.imshow(cv2.cvtColor(final_img, cv2.COLOR_BGR2RGB))
plt.title("Feature Matches")
plt.axis('off')

plt.show()
```

Kode tersebut digunakan untuk:
- menampilkan hasil akhir
- memberi judul gambar
- menghilangkan sumbu koordinat

### 📸 Hasil Feature Matching

![Feature Matching](Screenshot_Hasil_ORB/SS_4_Feature_Matching.png)

---

# ✅ Kesimpulan

Berdasarkan praktikum yang telah dilakukan, algoritma ORB berhasil digunakan untuk:
- mendeteksi keypoints
- membuat descriptor
- melakukan pencocokan fitur antar gambar

Metode ORB memiliki beberapa kelebihan:
- 🚀 cepat
- 💡 efisien
- 🔄 tahan terhadap rotasi
- 📏 dapat mendeteksi fitur pada berbagai skala

Hasil feature matching menunjukkan bahwa ORB mampu menemukan kemiripan fitur pada kedua gambar dengan baik.

---

# 📚 Referensi

## 📖 OpenCV Documentation
:contentReference[oaicite:0]{index=0}

## 📖 Python Documentation
:contentReference[oaicite:1]{index=1}

## 📖 Matplotlib Documentation
:contentReference[oaicite:2]{index=2}
