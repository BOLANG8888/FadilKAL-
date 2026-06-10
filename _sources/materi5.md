# membuat kordinat 

import matplotlib.pyplot as plt
import matplotlib.animation as animation
import numpy as np

# 1. Inisialisasi Data Koordinat Dasar
box_top_x = [2, 2, 3, 3, 2, 3, 2, 3]
box_top_y_init = [3, 4, 4, 3, 2, 2, 1, 1]

box_bottom_x = [2, 3, 2, 3, 2, 3, 2, 3]
box_bottom_y_init = [-3, -3, -4, -4, -1, -1, -2, -2]

# Persiapan Figure
fig, ax = plt.subplots(figsize=(8, 8))
ax.set_xlim(-1, 6)
ax.set_ylim(-6, 6)
ax.grid(True, linestyle=':', alpha=0.7)
ax.axhline(0, color='black', linewidth=2) # Garis target (sumbu X)
ax.set_title("Contoh gambar di bawah")

# Objek visual
scatter_top = ax.scatter(box_top_x, box_top_y_init, color='blue', s=100, label='Kotak Atas')
scatter_bottom = ax.scatter(box_bottom_x, box_bottom_y_init, color='red', s=100, label='Kotak Bawah')

# 2. Fungsi Animasi
def update(frame):
    # Menggunakan fungsi sin untuk membuat gerakan bolak-balik yang halus
    # frame akan bergerak dari 0 ke 1 dan kembali lagi
    t = (np.sin(frame / 10) + 1) / 2

    # Gerak titik atas mendekati 0
    new_y_top = [y * (1 - t) for y in box_top_y_init]
    scatter_top.set_offsets(np.c_[box_top_x, new_y_top])

    # Gerak titik bawah mendekati 0
    new_y_bottom = [y * (1 - t) for y in box_bottom_y_init]
    scatter_bottom.set_offsets(np.c_[box_bottom_x, new_y_bottom])

    return scatter_top, scatter_bottom

# 3. Menjalankan Animasi
# interval=20 membuat gerakan lebih mulus (50 FPS)
ani = animation.FuncAnimation(fig, update, frames=200, interval=20, blit=True)

plt.legend(loc='upper right')
plt.show()