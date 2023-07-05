# uas 202131080 aulia pravda 

Tentu! Izinkan saya menjelaskan fungsi perpustakaan yang diimpor:

1. `cv2` (OpenCV): OpenCV (Open Source Computer Vision Library) adalah pustaka populer untuk visi komputer dan tugas pemrosesan gambar. Ini menyediakan berbagai fungsi dan alat untuk memanipulasi dan memproses gambar, melakukan deteksi objek, melacak objek, dan banyak lagi.

2. `numpy` (np): NumPy adalah pustaka yang kuat untuk komputasi numerik dengan Python. Ini menyediakan struktur dan fungsi data yang efisien untuk menangani array dan matriks besar. Dalam tugas pemrosesan gambar, NumPy sering digunakan untuk operasi pada nilai piksel gambar dan perhitungan matematis.

3. `matplotlib.pyplot` (plt): Matplotlib adalah pustaka plot dengan Python yang menyediakan berbagai fungsi untuk membuat visualisasi. Modul `pyplot` menyediakan antarmuka seperti MATLAB untuk membuat plot, bagan, dan gambar. Ini biasanya digunakan untuk menampilkan gambar, menggambar histogram, grafik plot, dan memvisualisasikan data.

Singkatnya, `cv2` digunakan untuk tugas pemrosesan gambar dan visi komputer, `numpy` digunakan untuk komputasi numerik, dan `matplotlib.pyplot` digunakan untuk visualisasi dan plotting data.
Kode yang Anda berikan melakukan segmentasi gambar pada gambar "kiwi.jpg" menggunakan ambang warna dalam ruang warna HSV. Mari kita telusuri kode langkah demi langkah:

1. `img = cv2.imread('kiwi.jpg')`: Baris ini membaca file gambar "kiwi.jpg" dan menyimpannya dalam variabel `img`.

2. `hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)`: Baris ini mengonversi gambar BGR `img` ke ruang warna HSV dan menyimpannya dalam variabel `hsv_img`.

3. Ambang untuk pisang:
    - `lower_banana = np.array([20, 100, 100])`: Baris ini menentukan nilai ambang bawah untuk warna pisang dalam HSV.
    - `upper_banana = np.array([30, 255, 255])`: Baris ini menentukan nilai batas atas untuk warna pisang dalam HSV.
    - `mask_banana = cv2.inRange(hsv_img, lower_banana, upper_banana)`: Baris ini membuat topeng biner untuk piksel dalam `hsv_img` yang termasuk dalam kisaran yang ditentukan untuk warna pisang.

4. Ambang batas untuk apel dan kiwi:
    - Serupa dengan pisang, kode menentukan nilai ambang bawah dan atas untuk warna apel dan kiwi di HSV.
    - `mask_apple = cv2.inRange(hsv_img, lower_apple, upper_apple)`: Baris ini membuat topeng biner untuk piksel dalam `hsv_img` yang termasuk dalam kisaran yang ditentukan untuk warna apel.
    - `mask_kiwi = cv2.inRange(hsv_img, lower_kiwi, upper_kiwi)`: Baris ini membuat topeng biner untuk piksel dalam `hsv_img` yang termasuk dalam rentang yang ditentukan untuk warna kiwi.

5. Menerapkan topeng ke gambar asli:
    - `result_banana = cv2.bitwise_and(img, img, mask=mask_banana)`: Baris ini menerapkan `mask_banana` ke `img` menggunakan operasi bitwise AND, menghasilkan gambar yang hanya memiliki piksel dalam rentang warna pisang bisa dilihat.
    - Demikian pula, `result_apple` dan `result_kiwi` diperoleh dengan menerapkan mask yang sesuai ke `img` menggunakan operasi bitwise AND.

6. Operasi morfologis untuk membersihkan topeng:
    - `kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))`: Baris ini membuat elemen penataan bentuk elips dengan ukuran (5, 5).
    - `cleaned_mask_banana = cv2.morphologyEx(mask_banana, cv2.MORPH_OPEN, kernel)`: Baris ini melakukan pembukaan morfologis pada `mask_banana` menggunakan `kernel`, yang membantu menghilangkan noise dan menghaluskan topeng biner.
    - Demikian pula, `cleaned_mask_apple` dan `cleaned_mask_kiwi` diperoleh dengan menerapkan bukaan morfologis pada masker yang sesuai.

7. Menemukan kontur:
    - `contours_banana, _ = cv2.findContours(cleaned_mask_banana, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)`: Baris ini mencari kontur di `cleaned_mask_banana` menggunakan fungsi `cv2.findContours()`. Kontur mewakili batas-batas daerah pisang yang terdeteksi.
    - Demikian pula, `contours_apple` dan `contours_kiwi` diperoleh dengan mencari kontur pada masker yang dibersihkan untuk apel dan kiwi.

8. Menampilkan hasil:
    - Kode kemudian membuat a