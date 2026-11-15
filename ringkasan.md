| Skenario | Dice (rata-rata ± sb) | IoU (rata-rata ± sb) | Dice tiap ulangan |
|---|---|---|---|
| Tanpa augmentasi | 0.582 ± 0.010 | 0.465 ± 0.009 | 0.571, 0.595, 0.578 |
| Transformasi geometris | 0.625 ± 0.016 | 0.505 ± 0.014 | 0.608, 0.620, 0.646 |
| Variasi kualitas citra | 0.572 ± 0.036 | 0.450 ± 0.027 | 0.523, 0.585, 0.609 |
| Variasi karakteristik warna | 0.555 ± 0.055 | 0.435 ± 0.047 | 0.477, 0.593, 0.596 |


### Analisis Peta Kesalahan (Error Maps Analysis)

Berdasarkan visualisasi peta kesalahan (*error maps*) pada sampel hasil segmentasi U-Net:

1. **Kasus Positif Palsu (False Positive / FP)**:
   * **Temuan**: Model terkadang memprediksi area mukosa usus yang sehat atau lipatan lumen sebagai polip.
   * **Penyebab**: Pantulan cahaya lampu endoskopi (*specular reflection*) atau keberadaan cairan usus sering kali memiliki tingkat kecerahan dan tekstur yang mirip dengan batas jaringan polip.

2. **Kasus Negatif Palsu (False Negative / FN)**:
   * **Temuan**: Terjadi kegagalan deteksi (*under-segmentation*) terutama pada batas tepi polip datar (*flat polyps* / polip sessile).
   * **Penyebab**: Polip bertipe *sessile* memiliki batas kontras yang sangat halus dengan jaringan sekitarnya, sehingga fitur warna pada skenario augmentasi warna justru memperburuk deteksi area ini.

3. **Implikasi Biomedis**:
   * Penggunaan transformasi geometris terbukti menekan angka *False Negative* karena model dilatih mengenali kontur polip dari berbagai sudut tanpa terdistorsi oleh orientasi kamera endoskopi.
