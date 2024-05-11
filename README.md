# PCD_UTS_202231065_2024_ITPLN

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

img = cv2.imread("ujicoba.jpg")
plt.imshow(img)
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(rgb)
```
Pertama, kita mengimpor modul-modul yang diperlukan:

cv2: Modul OpenCV untuk memproses gambar.
numpy as np: NumPy digunakan untuk operasi array dan matriks.
matplotlib.pyplot as plt: Matplotlib digunakan untuk menampilkan gambar.
Kemudian, kita membaca gambar dengan menggunakan cv2.imread(). Fungsi ini membaca gambar dari file dan mengembalikan representasi dalam bentuk matriks piksel.

Setelah itu, kita menampilkan gambar pertama kali menggunakan plt.imshow(img). Perlu diingat bahwa meskipun kita menggunakan cv2 untuk membaca gambar, kita menggunakan plt.imshow() dari matplotlib untuk menampilkannya. Namun, langkah ini akan menampilkan warna dengan format yang salah karena OpenCV membaca gambar dalam urutan warna BGR (Blue, Green, Red), sedangkan matplotlib menggunakan urutan warna RGB (Red, Green, Blue).

Untuk memperbaiki urutan warna, kita gunakan cv2.cvtColor() untuk mengonversi gambar dari BGR ke RGB dengan menyediakan parameter cv2.COLOR_BGR2RGB. Hasilnya disimpan dalam variabel rgb.

Terakhir, kita tampilkan gambar yang sudah dikonversi warnanya menggunakan plt.imshow(rgb). Sekarang, gambar akan ditampilkan dengan warna yang benar.

```python
(baris, kolom)= rgb.shape[:2]
beta = 30 #bias untuk kecerahan
citra = np.zeros((baris, kolom, 3)) #np zeros = mengubah semua elemen array menjadi 0
 
for x in range(baris) :
    for y in range(kolom) :
        gyx = rgb[x,y] + beta
        citra[x,y] = gyx
citra = citra.astype(np.uint8)
 
fig, axs = plt.subplots(2,2, figsize=(15,5))
axs[0,0].imshow(rgb)
axs[0,1].hist(img.ravel(),256,[0,256])
axs[1,0].imshow(citra)
axs[1,1].hist(citra.ravel(),256,[0,256])
plt.show()
```
Kita mendapatkan dimensi gambar RGB menggunakan rgb.shape[:2] dan menyimpannya dalam variabel baris dan kolom.

Nilai beta (bias untuk kecerahan) ditentukan sebagai 30.

Membuat matriks kosong citra dengan ukuran yang sama dengan gambar, yaitu (baris, kolom, 3). Ini dilakukan menggunakan np.zeros() yang menghasilkan matriks dengan semua elemen 0.

Dilakukan loop traversing untuk setiap piksel dalam gambar:

Setiap piksel dalam gambar diambil dari matriks rgb dan ditambahkan dengan nilai beta untuk meningkatkan kecerahan. Hasilnya disimpan dalam matriks citra.
Perlu diingat bahwa penambahan dilakukan pada setiap kanal warna (R, G, B) secara terpisah.
Konversi tipe data matriks citra menjadi np.uint8 menggunakan astype(np.uint8). Hal ini diperlukan karena nilai piksel dalam gambar harus dalam rentang 0-255.

Setelah proses peningkatan kecerahan selesai, dilakukan plotting menggunakan plt.subplots() untuk menampilkan gambar asli dan histogramnya, serta gambar yang telah diubah kecerahannya dan histogramnya.

axs[0,0].imshow(rgb): Menampilkan gambar asli.
axs[0,1].hist(img.ravel(),256,[0,256]): Menampilkan histogram gambar asli.
axs[1,0].imshow(citra): Menampilkan gambar yang telah diubah kecerahannya.
axs[1,1].hist(citra.ravel(),256,[0,256]): Menampilkan histogram gambar yang telah diubah kecerahannya.
Terakhir, dipanggil plt.show() untuk menampilkan plot tersebut.

```python
plt.subplot(2, 2, 1)
plt.imshow(rgb)
plt.title('ASLI')

plt.subplot(2, 2, 2)
plt.imshow(rgb[:,:,0], cmap="gray")
plt.title('MERAH')

plt.subplot(2, 2, 3)
plt.imshow(rgb[:,:,1], cmap="gray")
plt.title('HIJAU')

plt.subplot(2, 2, 4)
plt.imshow(rgb[:,:,2], cmap="gray")
plt.title('BIRU')

plt.show()
```
plt.subplot(2, 2, 1): Ini membuat subplot pertama dari grid 2x2 (4 subplot secara keseluruhan) dan menetapkannya sebagai subplot saat ini. Gambar asli ditampilkan di subplot ini.

plt.imshow(rgb): Menampilkan gambar asli rgb dalam subplot pertama.

plt.title('ASLI'): Memberikan judul "ASLI" untuk subplot pertama.

plt.subplot(2, 2, 2): Membuat subplot kedua dari grid 2x2 dan menetapkannya sebagai subplot saat ini. Ini akan menampilkan saluran warna merah (R) dalam gambar.

plt.imshow(rgb[:,:,0], cmap="gray"): Menampilkan saluran warna merah dari gambar (rgb[:,:,0]) dalam skala abu-abu (grayscale), karena hanya menampilkan satu saluran warna, bukan gambar RGB penuh. Ini dilakukan dengan menambahkan parameter cmap="gray".

plt.title('MERAH'): Memberikan judul "MERAH" untuk subplot kedua.

Langkah-langkah 4-6 diulangi untuk menampilkan saluran warna hijau (G) dan biru (B) pada subplot ketiga dan keempat.

plt.subplot(2, 2, 3): Subplot ketiga untuk saluran warna hijau.

plt.imshow(rgb[:,:,1], cmap="gray"): Menampilkan saluran warna hijau dari gambar dalam skala abu-abu.

plt.title('HIJAU'): Memberikan judul "HIJAU" untuk subplot ketiga.

plt.subplot(2, 2, 4): Subplot keempat untuk saluran warna biru.

plt.imshow(rgb[:,:,2], cmap="gray"): Menampilkan saluran warna biru dari gambar dalam skala abu-abu.

plt.title('BIRU'): Memberikan judul "BIRU" untuk subplot keempat.

Terakhir, plt.show() dipanggil untuk menampilkan subplot-subplot yang telah disusun dengan gambar-gambar dan judul-judulnya.

```python
merah=citra[:,:,0]
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([merah],[0],None,[256],[0,256])
axs[0].imshow(merah, cmap='gray')
axs[1].plot(hist)
plt.show()
```
merah = citra[:,:,0]: Di sini, kita mengambil saluran warna merah dari gambar yang telah diubah kecerahannya (citra). Karena gambar yang diubah kecerahannya disimpan dalam format RGB, saluran warna merah terletak pada indeks 0 dari sumbu kedua.

fig, axs = plt.subplots(1,2, figsize=(15,5)): Membuat suatu figure (gambar) yang memiliki dua subplot sejajar dengan ukuran total (15,5).

hist = cv2.calcHist([merah],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna merah menggunakan fungsi cv2.calcHist(). Parameter pertama adalah list dari gambar asalnya (merah), parameter kedua adalah indeks dari channel warna yang ingin dihitung histogramnya (dalam kasus ini 0, karena kita hanya punya satu channel yaitu channel merah), parameter ketiga adalah mask, yang di sini kita tidak menggunakan (None), parameter keempat adalah jumlah bin (256), dan parameter kelima adalah rentang nilai piksel yang diinginkan (0 sampai 256).

axs[0].imshow(merah, cmap='gray'): Menampilkan saluran warna merah pada subplot pertama dengan menggunakan colormap 'gray', karena kita hanya menampilkan satu channel warna dan bukan gambar RGB penuh.

axs[1].plot(hist): Menampilkan histogram yang telah dihitung pada subplot kedua dengan menggunakan plt.plot(). Ini akan menampilkan grafik garis yang menunjukkan distribusi intensitas warna merah di dalam gambar.

plt.show(): Menampilkan plot histogram dan gambar pada subplot yang telah dibuat.

```python
hijau=citra[:,:,1] 
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([hijau],[0],None,[256],[0,256])
axs[0].imshow(hijau, cmap='gray')
axs[1].plot(hist)
plt.show()
```
hijau = citra[:,:,1]: Di sini, kita mengambil saluran warna hijau dari gambar yang telah diubah kecerahannya (citra). Saluran warna hijau terletak pada indeks 1 dari sumbu kedua dalam representasi gambar RGB.

fig, axs = plt.subplots(1,2, figsize=(15,5)): Membuat suatu figure (gambar) yang memiliki dua subplot sejajar dengan ukuran total (15,5).

hist = cv2.calcHist([hijau],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna hijau menggunakan fungsi cv2.calcHist(). Parameter pertama adalah list dari gambar asalnya (hijau), parameter kedua adalah indeks dari channel warna yang ingin dihitung histogramnya (dalam kasus ini 0, karena kita hanya punya satu channel yaitu channel hijau), parameter ketiga adalah mask, yang di sini kita tidak menggunakan (None), parameter keempat adalah jumlah bin (256), dan parameter kelima adalah rentang nilai piksel yang diinginkan (0 sampai 256).

axs[0].imshow(hijau, cmap='gray'): Menampilkan saluran warna hijau pada subplot pertama dengan menggunakan colormap 'gray', karena kita hanya menampilkan satu channel warna dan bukan gambar RGB penuh.

axs[1].plot(hist): Menampilkan histogram yang telah dihitung pada subplot kedua dengan menggunakan plt.plot(). Ini akan menampilkan grafik garis yang menunjukkan distribusi intensitas warna hijau di dalam gambar.

plt.show(): Menampilkan plot histogram dan gambar pada subplot yang telah dibuat.

```python
biru=citra[:,:,2] 
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([biru],[0],None,[256],[0,256])
axs[0].imshow(biru, cmap='gray')
axs[1].plot(hist)
plt.show()
```
biru = citra[:,:,2]: Di sini, kita mengambil saluran warna biru dari gambar yang telah diubah kecerahannya (citra). Saluran warna biru terletak pada indeks 2 dari sumbu kedua dalam representasi gambar RGB.

fig, axs = plt.subplots(1,2, figsize=(15,5)): Membuat suatu figure (gambar) yang memiliki dua subplot sejajar dengan ukuran total (15,5).

hist = cv2.calcHist([biru],[0],None,[256],[0,256]): Menghitung histogram dari saluran warna biru menggunakan fungsi cv2.calcHist(). Parameter pertama adalah list dari gambar asalnya (biru), parameter kedua adalah indeks dari channel warna yang ingin dihitung histogramnya (dalam kasus ini 0, karena kita hanya punya satu channel yaitu channel biru), parameter ketiga adalah mask, yang di sini kita tidak menggunakan (None), parameter keempat adalah jumlah bin (256), dan parameter kelima adalah rentang nilai piksel yang diinginkan (0 sampai 256).

axs[0].imshow(biru, cmap='gray'): Menampilkan saluran warna biru pada subplot pertama dengan menggunakan colormap 'gray', karena kita hanya menampilkan satu channel warna dan bukan gambar RGB penuh.

axs[1].plot(hist): Menampilkan histogram yang telah dihitung pada subplot kedua dengan menggunakan plt.plot(). Ini akan menampilkan grafik garis yang menunjukkan distribusi intensitas warna biru di dalam gambar.

plt.show(): Menampilkan plot histogram dan gambar pada subplot yang telah dibuat.

```python
gray = cv2.cvtColor(citra, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('none')

(thresh, binary2) = cv2.threshold(gray, 105,255, cv2.THRESH_BINARY)
axs[0,1].imshow(binary2, cmap = 'binary')
axs[0,1].set_title('blue')

(thresh, binary3) = cv2.threshold(gray, 125, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('red-blue')

(thresh, binary4) = cv2.threshold(gray, 147, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RGB')
```
gray = cv2.cvtColor(citra, cv2.COLOR_RGB2GRAY): Mengonversi gambar citra dari format RGB ke grayscale menggunakan cv2.cvtColor(). Hasilnya disimpan dalam variabel gray, yang merupakan representasi gambar dalam skala abu-abu.

fig, axs = plt.subplots(2, 2, figsize=(10,10)): Membuat suatu figure (gambar) yang memiliki empat subplot dalam grid 2x2 dengan ukuran total (10,10).

Setiap subplot akan menampilkan hasil thresholding yang berbeda dari gambar grayscale:

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY): Thresholding tanpa melakukan perubahan apapun. thresh tidak digunakan (oleh karena itu diset 0) dan binary1 akan menjadi gambar biner yang diperoleh dari thresholding. cv2.THRESH_BINARY digunakan untuk menunjukkan bahwa setiap piksel yang lebih besar dari 0 akan diubah menjadi 255 (putih), yang kurang dari 0 tetap 0 (hitam).

(thresh, binary2) = cv2.threshold(gray, 105, 255, cv2.THRESH_BINARY): Thresholding menggunakan nilai ambang 105. Piksel dengan intensitas yang lebih besar dari 105 akan menjadi putih (255), sedangkan piksel dengan intensitas yang lebih rendah tetap hitam (0).

(thresh, binary3) = cv2.threshold(gray, 125, 255, cv2.THRESH_BINARY): Thresholding menggunakan nilai ambang 125. Pada kasus ini, nilai ambang yang lebih tinggi dipilih, sehingga lebih banyak piksel yang akan diubah menjadi putih.

(thresh, binary4) = cv2.threshold(gray, 147, 255, cv2.THRESH_BINARY): Thresholding menggunakan nilai ambang 147. Pada subplot ini, nilai ambang yang lebih tinggi lagi dipilih, sehingga lebih sedikit piksel yang akan diubah menjadi putih.

axs[i,j].imshow(binary, cmap='binary'): Menampilkan gambar biner dalam subplot yang sesuai dengan menggunakan colormap 'binary', di mana warna putih menunjukkan nilai piksel yang lebih tinggi (255) dan warna hitam menunjukkan nilai piksel yang lebih rendah (0).

axs[i,j].set_title('title'): Menetapkan judul untuk setiap subplot sesuai dengan jenis thresholding yang digunakan.

Terakhir, plt.show() dipanggil untuk menampilkan gambar-gambar biner pada subplot-subplot yang telah dibuat.
