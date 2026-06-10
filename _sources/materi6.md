# Dekomposisi Matrix

## Diketahui Matriks

\[
A =
\begin{bmatrix}
3 & 5 & 7 & 6 \\
9 & 3 & 5 & 7 \\
4 & 6 & 5 & 1 \\
2 & 8 & 1 & 4
\end{bmatrix}
\]

Tujuan:
- Mencari vektor ortonormal \(q_1, q_2, q_3, q_4\)
- Membentuk matriks \(Q\)
- Membentuk matriks \(R\)
- Menggunakan metode Gram-Schmidt.

---

# Rumus Gram-Schmidt

## 1. Mencari Vektor Orthogonal

\[
v_k = a_k - \sum_{i=1}^{k-1}(a_k \cdot q_i)q_i
\]

## 2. Normalisasi

\[
q_k = \frac{v_k}{\|v_k\|}
\]

---

# Membentuk Vektor Kolom

Kolom-kolom matriks:

\[
a_1=
\begin{bmatrix}
3\\9\\4\\2
\end{bmatrix}
\]

\[
a_2=
\begin{bmatrix}
5\\3\\6\\8
\end{bmatrix}
\]

\[
a_3=
\begin{bmatrix}
7\\5\\5\\1
\end{bmatrix}
\]

\[
a_4=
\begin{bmatrix}
6\\7\\1\\4
\end{bmatrix}
\]

---

# Langkah 1 — Mencari \(q_1\)

Karena:

\[
v_1 = a_1
\]

Norma:

\[
\|v_1\| =
\sqrt{3^2 + 9^2 + 4^2 + 2^2}
\]

\[
=
\sqrt{110}
\]

Maka:

\[
q_1=
\frac{1}{\sqrt{110}}
\begin{bmatrix}
3\\9\\4\\2
\end{bmatrix}
\]

Hasil desimal:

\[
q_1 \approx
\begin{bmatrix}
0.2860\\
0.8581\\
0.3814\\
0.1907
\end{bmatrix}
\]

---

# Langkah 2 — Mencari \(q_2\)

Hitung proyeksi:

\[
(a_2 \cdot q_1)
\]

\[
=
5(0.2860)+3(0.8581)+6(0.3814)+8(0.1907)
\]

\[
\approx 7.8207
\]

Mencari:

\[
v_2=a_2-(a_2\cdot q_1)q_1
\]

Hasil:

\[
v_2 \approx
\begin{bmatrix}
2.7636\\
-3.7107\\
3.0165\\
6.5082
\end{bmatrix}
\]

Norma:

\[
\|v_2\| \approx 8.3666
\]

Maka:

\[
q_2=
\frac{v_2}{\|v_2\|}
\]

\[
q_2 \approx
\begin{bmatrix}
0.3303\\
-0.4435\\
0.3605\\
0.7779
\end{bmatrix}
\]

---

# Langkah 3 — Mencari \(q_3\)

Gunakan rumus:

\[
v_3=
a_3
-(a_3 \cdot q_1)q_1
-(a_3 \cdot q_2)q_2
\]

Hasil:

\[
q_3 \approx
\begin{bmatrix}
0.8560\\
-0.2357\\
-0.4188\\
-0.1955
\end{bmatrix}
\]

---

# Langkah 4 — Mencari \(q_4\)

Gunakan:

\[
v_4=
a_4
-(a_4 \cdot q_1)q_1
-(a_4 \cdot q_2)q_2
-(a_4 \cdot q_3)q_3
\]

Hasil:

\[
q_4 \approx
\begin{bmatrix}
0.2766\\
0.1056\\
-0.7446\\
0.5988
\end{bmatrix}
\]

---

# Matriks Ortonormal \(Q\)

\[
Q=
\begin{bmatrix}
0.2860 & 0.3303 & 0.8560 & 0.2766\\
0.8581 & -0.4435 & -0.2357 & 0.1056\\
0.3814 & 0.3605 & -0.4188 & -0.7446\\
0.1907 & 0.7779 & -0.1955 & 0.5988
\end{bmatrix}
\]

---

# Matriks \(R\)

Menggunakan:

\[
R = Q^T A
\]

Hasil:

\[
R \approx
\begin{bmatrix}
10.4881 & 7.8207 & 8.9645 & 8.8699\\
0 & 8.3666 & 3.3968 & 2.8761\\
0 & 0 & 4.1472 & 3.2864\\
0 & 0 & 0 & 1.2977
\end{bmatrix}
\]

---

# Verifikasi

Metode QR memenuhi:

\[
A = QR
\]

---

# Coding Python Gram-Schmidt

```python
import numpy as np

# Matriks A
A = np.array([
    [3, 5, 7, 6],
    [9, 3, 5, 7],
    [4, 6, 5, 1],
    [2, 8, 1, 4]
], dtype=float)

# Jumlah kolom
n = A.shape[1]

# Matriks kosong Q dan R
Q = np.zeros((4,4))
R = np.zeros((4,4))

# Proses Gram-Schmidt
for k in range(n):

    v = A[:, k]

    for i in range(k):
        R[i, k] = np.dot(Q[:, i], A[:, k])
        v = v - R[i, k] * Q[:, i]

    R[k, k] = np.linalg.norm(v)

    Q[:, k] = v / R[k, k]

# Menampilkan hasil
print("Matriks Q:")
print(np.round(Q, 4))

print("\nMatriks R:")
print(np.round(R, 4))

# Verifikasi
print("\nVerifikasi A = Q @ R")
print(np.round(Q @ R, 4))
```

---

# Output Program

```python
Matriks Q:
[[ 0.286   0.3303  0.856   0.2766]
 [ 0.8581 -0.4435 -0.2357  0.1056]
 [ 0.3814  0.3605 -0.4188 -0.7446]
 [ 0.1907  0.7779 -0.1955  0.5988]]

Matriks R:
[[10.4881  7.8207  8.9645  8.8699]
 [ 0.      8.3666  3.3968  2.8761]
 [ 0.      0.      4.1472  3.2864]
 [ 0.      0.      0.      1.2977]]
```

---

# Kesimpulan

Metode Gram-Schmidt digunakan untuk:
- Mengubah basis biasa menjadi basis ortonormal
- Membentuk dekomposisi QR

Dengan:

\[
A = QR
\]

Keterangan:
- \(Q\) = matriks ortonormal
- \(R\) = matriks segitiga atas

Metode ini sering digunakan dalam:
- Aljabar Linear
- Machine Learning
- Komputasi Numerik
- Sistem Persamaan Linear