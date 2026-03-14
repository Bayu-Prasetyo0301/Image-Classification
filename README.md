# Proyek Klasifikasi Gambar: Animal Faces

Proyek ini merupakan sistem klasifikasi gambar berbasis **Deep Learning** yang dirancang untuk mengenali wajah hewan ke dalam tiga kategori utama: **Kucing (Cat)**, **Anjing (Dog)**, dan **Hewan Liar (Wild)**. Fokus utama proyek ini adalah mencapai akurasi tinggi (>96%) dengan generalisasi model yang baik melalui teknik augmentasi dan optimasi hyperparameter.

---

## 👤 Informasi Pengembang
* **Nama:** Bayu Prasetyo
* **Email:** bayupras0301@gmail.com
* **ID Dicoding:** bayupras0301
* **Dataset Link:** https://www.kaggle.com/datasets/andrewmvd/animal-faces

---

## 📊 Ringkasan Dataset
* **Sumber:** Animal Faces Dataset (Kaggle)
* **Kelas:** 3 (cat, dog, wild)
* **Distribusi Data:** Dataset dibagi secara stratified menjadi:
    * **Data Pelatihan (70%):** 11.291 gambar.
    * **Data Validasi (20%):** 3.242 gambar.
    * **Data Pengujian (10%):** 1.597 gambar.

---

## 🛠 Preprocessing & Augmentasi Data
Untuk mencegah *overfitting*, model menggunakan `ImageDataGenerator` dengan teknik augmentasi yang ekstensif:
* **Rescale:** 1./255 (Normalisasi piksel).
* **Augmentasi:** Rotasi (30°), Width/Height Shift (0.2), Zoom (0.2), Horizontal Flip, dan Shear Range (0.2).

---

## 🧠 Arsitektur Model
Model dibangun menggunakan **CNN (Convolutional Neural Network)** dengan struktur sebagai berikut:
1.  **Input Layer:** 150x150 piksel (RGB).
2.  **Hidden Layers:** 3 blok `Conv2D` + `MaxPooling2D` disertai `BatchNormalization` untuk mempercepat konvergensi.
3.  **Fully Connected:** 512 unit `Dense` layer dengan `Dropout(0.5)` untuk regulasi.
4.  **Output Layer:** `Dense` layer dengan aktivasi **Softmax** untuk klasifikasi 3 kelas.

---

## 🚀 Strategi Pelatihan
* **Optimizer:** Adam dengan learning rate awal 0.0001.
* **Loss Function:** Categorical Crossentropy.
* **Custom Callbacks:** * `DualAccuracyCallback`: Menghentikan pelatihan secara otomatis jika Akurasi Training DAN Validasi sudah mencapai target 96%.
    * `ReduceLROnPlateau`: Mengurangi learning rate jika akurasi validasi tidak kunjung membaik.

---

## 📈 Hasil Akhir (Final Metrics)
Berdasarkan proses pelatihan terakhir, model mencapai performa yang sangat stabil:

| Dataset | Akurasi |
| :--- | :--- |
| **Training** | 96.06% |
| **Validasi** | 96.45% |
| **Testing** | 95.99% |

---

## 📦 Ekspor Model & Deployment
Model telah diekspor ke dalam tiga format berbeda untuk mendukung berbagai skenario deployment:
1.  **SavedModel (.pb):** Untuk deployment di sisi server.
2.  **TensorFlow Lite (.tflite):** Dioptimalkan untuk aplikasi Mobile/Android.
3.  **TensorFlow.js:** Untuk aplikasi berbasis Web (browser).
