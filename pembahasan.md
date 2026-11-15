### Pembahasan Hasil Eksperimen

Berdasarkan pengujian segmentasi polip pada citra kolonoskopi dataset Kvasir-SEG menggunakan U-Net, penggunaan teknik augmentasi memberikan dampak yang bervariasi terhadap performa model:

1. **Keberhasilan Transformasi Geometris (Dice: 0,625 ± 0,016 | IoU: 0,505 ± 0,014)**
   * Transformasi geometris (horizontal flip, vertical flip, dan rotasi hingga 180°) berhasil meningkatkan performa model secara signifikan dibandingkan skenario tanpa augmentasi (Dice: 0,582 ± 0,010 | IoU: 0,465 ± 0,009).
   * **Analisis Biomedis & Teknis**: Pada citra kolonoskopi nyata, kamera endoskopi bergerak secara dinamis di dalam saluran cerna. Akibatnya, polip tidak memiliki orientasi baku. Augmentasi geometris melatih model U-Net agar *invariant* terhadap perubahan posisi dan sudut pandang tanpa merusak struktur morfologi asli polip.

2. **Penurunan Performa pada Variasi Kualitas Citra (Dice: 0,572 ± 0,036)**
   * Penyesuaian *brightness*, *contrast*, dan *Gaussian blur* justru menghasilkan rata-rata Dice yang sedikit lebih rendah dibanding tanpa augmentasi.
   * **Analisis Biomedis & Teknis**: Polip sering kali diidentifikasi berdasarkan tekstur permukaan dan ketajaman batas antara batas jaringan polip dengan mukosa usus. Efek *blur* atau kontras ekstrem berisiko menghapus tekstur halus tersebut, sehingga model mengalami kendala (*under-segmentation*) pada batas polip.

3. **Dampak Negatif Variasi Warna (Dice: 0,555 ± 0,555)**
   * Manipulasi *saturation* dan *hue* memberikan performa paling rendah serta tingkat variansi/simpangan baku yang paling tinggi.
   * **Analisis Biomedis & Teknis**: Warna kemerahan/vaskularisasi pada mukosa merupakan petunjuk visual penting dalam dataset Kvasir-SEG. Perubahan *hue* dan *saturation* yang terlalu jauh mengubah vaskularisasi alami menjadi tidak realistis, yang menguraikan alasan mengapa augmentasi warna kurang cocok untuk tugas segmentasi medis ini.
