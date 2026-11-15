### Konsep Dasar U-Net & Segmentasi Citra Biomedis

*Disusun oleh: Bintang Putra Gunawan*

#### 1. Pengenalan Segmentasi Citra Medis
Segmentasi citra biomedis bertujuan untuk mengklasifikasikan setiap piksel (*pixel-wise classification*) pada citra medis ke dalam kategori tertentu (dalam proyek ini: piksel polip vs. latar belakang/mukosa usus). 

#### 2. Arsitektur U-Net
U-Net merupakan arsitektur Convolutional Neural Network (CNN) berstruktur simetris berbentuk huruf "U" yang dirancang khusus untuk segmentasi citra medis. Arsitektur ini terdiri dari dua bagian utama:
1. **Contracting Path (Encoder)**:
   * Berfungsi mengekstraksi fitur konteks visual dari citra input (ukuran 128 × 128 piksel).
   * Menggunakan operasi konvolusi berulang (`Conv2d`), fungsi aktivasi `ReLU`, dan pemangkasan ukuran spasial melalui `MaxPool2d`.
2. **Expanding Path (Decoder)**:
   * Berfungsi mengonstruksi kembali resolusi spasial citra untuk menghasilkan *segmentation mask* akhir.
   * Menggunakan operasi *upsampling* (`ConvTranspose2d`) untuk mengembalikan ukuran citra ke dimensi semula.

#### 3. Peran Kunci Skip Connections
Salah satu keunggulan utama U-Net terletak pada fitur **Skip Connections**, yaitu menghubungkan peta fitur (*feature maps*) langsung dari lapisan *Encoder* ke lapisan *Decoder* pada tingkat resolusi yang sama. 
* **Fungsi Biomedis**: Memastikan informasi detail spasial berskala halus (seperti tekstur dan batas tepi polip) tidak hilang akibat proses kompresi di *Encoder*, sehingga batas segmentasi polip dapat terdeteksi secara akurat.

#### 4. Metrik Evaluasi Performa
* **Dice Score (F1-Score Piksel)**: Mengukur tingkat kemiripan/tumpang tindih antara mask prediksi model dengan ground truth mask polip.
* **IoU (Intersection over Union)**: Mengukur rasio irisan terhadap gabungan area polip sebenarnya dan area prediksi.
