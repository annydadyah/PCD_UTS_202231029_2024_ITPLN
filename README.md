# PCD_UTS_202231029_2024_ITPLN
Nama : Annyda Dyah Kusuma

NIM : 202231029

---
# Pengolahan Citra

Citra adalah salah satu bentuk data yang penting bagi manusia, selain teks, suara, dan video. Ketersediaan informasi visual ini tidak hanya penting dalam komunikasi antarmanusia, tetapi juga dalam interaksi manusia dengan mesin. Namun, penting untuk diingat bahwa interpretasi citra dapat bervariasi antara individu karena sifatnya yang subjektif. Artinya, nilai informasi yang terkandung dalam sebuah citra dapat berbeda-beda tergantung pada kebutuhan dan perspektif masing-masing orang. Oleh karena itu, diperlukan pengolahan citra untuk menghasilkan informasi visual yang sesuai dengan kebutuhan penggunanya.

---
# Tahapan Pengolahan Citra Berdasarkan Soal

1. Persiapan Citra:

Kodingan dimulai dengan mengimpor library yang dibutuhkan, yaitu cv2 (OpenCV) untuk pemrosesan citra, numpy untuk operasi numerik, dan matplotlib.pyplot untuk visualisasi. Kemudian, kodingan membaca citra "c1.jpg" menggunakan fungsi cv2.imread(). Dimensi citra (baris dan kolom) diperoleh dari atribut img.shape. Selanjutnya, kodingan mengonversi citra dari ruang warna BGR (Blue-Green-Red) ke RGB menggunakan fungsi cv2.cvtColor(). Konversi ini dilakukan karena sistem warna yang digunakan oleh OpenCV adalah BGR, sedangkan matplotlib menggunakan RGB.

2. Memisahkan Warna (Warna Merah, Hijau, dan Biru):

Setelah persiapan citra, kodingan memisahkan setiap kanal warna (merah, hijau, dan biru) dari citra menggunakan indeks pada dimensi ketiga (img[:,:,channel_index]). Untuk setiap kanal warna, kodingan membuat citra baru yang hanya menampilkan kanal warna tersebut menggunakan fungsi cv2.merge(). Selanjutnya, kodingan membuat subplot dengan ukuran 2x2 menggunakan plt.subplots() dan menampilkan citra asli, histogram citra asli, citra satu kanal, dan histogram citra satu kanal pada setiap subplot menggunakan imshow() dan hist().

3. Analisis Hasil Histogram:

Histogram menunjukkan distribusi intensitas piksel pada citra. Histogram citra asli menunjukkan kombinasi intensitas dari ketiga kanal warna (merah, hijau, dan biru), sedangkan histogram citra merah, hijau, dan biru menunjukkan distribusi intensitas piksel untuk masing-masing kanal warna secara terpisah. Analisis histogram dapat memberikan informasi tentang karakteristik citra, seperti tingkat kecerahan, kontras, dan distribusi warna.

4. Proses Menemukan Nilai Batas Ambang:

Membuat citra baru yang menggabungkan kanal warna biru dan merah menggunakan cv2.merge(). Citra gabungan ini kemudian dikonversi ke grayscale menggunakan cv2.cvtColor() dengan konversi BGR2GRAY. Selanjutnya, membuat citra kosong (hitam) dengan ukuran yang sama seperti citra asli menggunakan np.zeros_like(). Mengonversi citra satu kanal (merah, hijau, biru, citra asli, dan citra kosong) ke grayscale. Kemudian, kodingan melakukan operasi thresholding adaptif pada citra grayscale menggunakan cv2.threshold() dengan metode THRESH_BINARY dan THRESH_OTSU. Metode THRESH_OTSU digunakan untuk menentukan nilai ambang batas secara otomatis berdasarkan analisis histogram citra. Nilai ambang batas (threshold value) yang diperoleh dicetak untuk setiap citra.
Selanjutnya, kodingan menggabungkan nama citra dan nilai ambang batas dalam bentuk list of tuples. Kemudian, list of tuples diurutkan berdasarkan nilai ambang batas menggunakan sorted() dan key function lambda. Hasil pengurutan dicetak, menampilkan nama citra dan nilai ambang batas yang telah diurutkan.
Terakhir, melakukan operasi invert (negative) pada citra biner hasil thresholding menggunakan cv2.bitwise_not(). Citra invert kemudian ditampilkan pada subplot dengan ukuran 2x2 menggunakan imshow().

---
# Analisis Hasil Histogram

Dalam membuat histogram, saya melakukan percobaan dengan mengganti interval dari histogram. Hal ini bertujuan untuk mempermudah menganalisis perbedaan signifikan antara histogram pada citra asli dengan citra yang telah dipisah warnanya.

1. Hasil Analisis Histogram Citra Merah:

Histogram citra merah menunjukkan distribusi intensitas piksel untuk kanal warna merah saja. Jika dibandingkan dengan histogram citra asli, terlihat perbedaan yang signifikan. Histogram citra asli memiliki distribusi intensitas yang lebih luas, mencakup rentang nilai piksel dari 0 hingga 255 untuk ketiga kanal warna (merah, hijau, dan biru). Sementara itu, histogram citra merah menunjukkan penumpukan intensitas pada rentang nilai yang lebih rendah, terutama pada nilai-nilai di sekitar 0-10. Hal ini mengindikasikan bahwa citra merah memiliki banyak piksel dengan intensitas warna merah yang rendah. Perbedaan ini menunjukkan bahwa citra asli memiliki kombinasi warna yang lebih beragam, sedangkan citra merah hanya menampilkan informasi tentang intensitas warna merah saja, yang sebagian besar terkonsentrasi pada nilai-nilai yang lebih rendah.

2. Hasil Analisis Histogram Citra Hijau:

Histogram citra hijau juga menunjukkan perbedaan yang signifikan jika dibandingkan dengan histogram citra asli. Histogram citra hijau menampilkan penumpukan intensitas pada rentang nilai yang lebih tinggi, terutama pada nilai-nilai di sekitar 200-250. Hal ini mengindikasikan bahwa citra memiliki banyak piksel dengan intensitas warna hijau yang tinggi. Sementara itu, histogram citra asli menunjukkan distribusi intensitas yang lebih merata untuk semua kanal warna (merah, hijau, dan biru). Perbedaan ini disebabkan karena pada citra hijau, informasi intensitas piksel untuk kanal warna merah dan biru dihilangkan, sehingga hanya intensitas piksel untuk kanal warna hijau yang dipertahankan.

3. Hasil Analisis Histogram Citra Biru:

Histogram citra biru menampilkan penumpukan intensitas pada rentang nilai yang lebih rendah, terutama pada nilai-nilai di sekitar 0-50. Hal ini mengindikasikan bahwa citra memiliki banyak piksel dengan intensitas warna biru yang rendah. Sementara itu, histogram citra asli menunjukkan distribusi intensitas yang lebih merata untuk semua kanal warna (merah, hijau, dan biru). Perbedaan ini disebabkan karena pada citra biru, informasi intensitas piksel untuk kanal warna merah dan hijau dihilangkan, sehingga hanya intensitas piksel untuk kanal warna biru yang dipertahankan.

---
# Hasil Nilai Ambang

Metode thresholding Otsu adalah algoritma yang digunakan untuk menentukan nilai ambang batas secara otomatis berdasarkan analisis histogram citra. Algoritma ini berupaya mencari nilai ambang batas yang memaksimalkan variansi antar kelas (between-class variance) dan meminimalkan variansi dalam kelas (within-class variance) dari distribusi intensitas piksel dalam citra.

Berikut adalah hasil pengurutan nilai batas ambang dari yang terkecil :

1. None -> Nilai ambang batas = 0.0
2. Merah -> Nilai ambang batas = 119.0
3. Hijau -> Nilai ambang batas = 133.0
4. Biru -> Nilai ambang batas = 142.0
5. RGB -> Nilai ambang batas = 148.0

Berikut adalah penjelasan rinci mengenai alasan mengapa diperoleh urutan nilai ambang batas seperti yang ditampilkan:

1. None -> Nilai ambang batas = 0.0:

Pada citra kosong (none), semua piksel memiliki nilai intensitas yang sama, yaitu 0 (hitam). Karena tidak ada variasi intensitas dalam citra, maka variansi dalam kelas adalah 0, dan variansi antar kelas juga menjadi 0 untuk semua kemungkinan nilai ambang batas. Oleh karena itu, metode Otsu memilih nilai ambang batas 0.0, yang merupakan nilai default karena tidak ada pemisahan yang diperlukan pada citra yang seragam.

2. Merah -> Nilai ambang batas = 119.0:

Citra merah hanya memiliki informasi intensitas dari kanal warna merah saja. Histogram dari citra merah menunjukkan distribusi intensitas piksel yang cenderung rendah hingga menengah. Metode Otsu menganalisis histogram ini dan menemukan nilai ambang batas 119.0 sebagai nilai yang memaksimalkan variansi antar kelas dan meminimalkan variansi dalam kelas. Nilai ini membagi citra menjadi dua kelompok: piksel dengan intensitas di bawah 119.0 dan piksel dengan intensitas di atas 119.0.

3. Hijau -> Nilai ambang batas = 133.0:

Citra hijau hanya memiliki informasi intensitas dari kanal warna hijau saja. Histogram dari citra hijau menunjukkan distribusi intensitas piksel yang cenderung lebih tinggi dibandingkan dengan citra merah. Metode Otsu menganalisis histogram ini dan menemukan nilai ambang batas 133.0 sebagai nilai yang memaksimalkan variansi antar kelas dan meminimalkan variansi dalam kelas untuk citra hijau.

4. Biru -> Nilai ambang batas = 142.0:

Citra biru hanya memiliki informasi intensitas dari kanal warna biru saja. Histogram dari citra biru menunjukkan distribusi intensitas piksel yang cenderung lebih tinggi dibandingkan dengan citra merah dan hijau. Metode Otsu menganalisis histogram ini dan menemukan nilai ambang batas 142.0 sebagai nilai yang memaksimalkan variansi antar kelas dan meminimalkan variansi dalam kelas untuk citra biru.

5. RGB -> Nilai ambang batas = 148.0:

Citra RGB merupakan kombinasi dari ketiga kanal warna (merah, hijau, dan biru). Histogram dari citra RGB menunjukkan distribusi intensitas piksel yang lebih kompleks dan memiliki rentang yang lebih luas dibandingkan dengan citra tunggal kanal warna. Metode Otsu menganalisis histogram ini dan menemukan nilai ambang batas 148.0 sebagai nilai yang memaksimalkan variansi antar kelas dan meminimalkan variansi dalam kelas untuk citra RGB.

Perbedaan nilai ambang batas yang diperoleh untuk setiap citra atau kanal warna disebabkan oleh perbedaan distribusi intensitas piksel pada masing-masing citra atau kanal. Semakin tinggi nilai ambang batas, semakin banyak piksel yang diklasifikasikan sebagai objek (intensitas di atas ambang batas) dan semakin sedikit piksel yang diklasifikasikan sebagai latar belakang (intensitas di bawah ambang batas).

Metode Otsu berupaya menemukan nilai ambang batas yang optimal untuk memisahkan objek dari latar belakang berdasarkan distribusi intensitas piksel dalam citra. Ini memungkinkan untuk mengekstraksi objek atau fitur yang diinginkan dari citra dengan cara yang otomatis dan efisien.

---
# Teori Yang Terkait Dengan Project

1. Pemisahan Kanal Warna RGB (Red, Green, Blue):

Citra digital berwarna biasanya terdiri dari kombinasi tiga kanal warna dasar, yaitu merah (red), hijau (green), dan biru (blue). Pada kode program ini, citra input dibaca dalam format BGR (Blue-Green-Red), kemudian dikonversi ke format RGB. Selanjutnya, setiap kanal warna dipisahkan menggunakan pemilihan elemen pada ketiga dimensi array citra. Hasil pemisahan ini menghasilkan tiga citra yang masing-masing hanya berisi informasi warna tunggal (merah, hijau, atau biru).

Pemisahan kanal warna berguna untuk melakukan analisis atau pengolahan yang spesifik pada setiap komponen warna secara terpisah. Misalnya, untuk meningkatkan kontras atau mengubah distribusi intensitas pada salah satu kanal warna tertentu.

2. Visualisasi Citra dan Histogram:

Pada kode program, setelah memisahkan kanal warna, setiap kanal warna ditampilkan secara visual menggunakan library Matplotlib. Selain itu, histogram dari setiap kanal warna juga ditampilkan untuk memberikan representasi visual dari distribusi intensitas piksel pada masing-masing kanal.

Histogram adalah grafik yang menggambarkan distribusi frekuensi nilai intensitas piksel dalam citra. Sumbu horizontal mewakili nilai intensitas piksel, sedangkan sumbu vertikal mewakili jumlah piksel dengan intensitas tertentu. Histogram berguna untuk menganalisis karakteristik kecerahan, kontras, dan distribusi intensitas piksel dalam citra.

3. Penggabungan Kanal Warna:

Setelah memisahkan dan memvisualisasikan kanal warna secara individual, kode program juga menggabungkan kembali kanal warna tertentu untuk membentuk citra baru. Misalnya, menggabungkan kanal merah dan biru untuk membentuk citra dengan tulisan berwarna putih pada latar belakang hitam. Penggabungan kanal warna dilakukan menggunakan fungsi cv2.merge() dari library OpenCV.

Penggabungan kanal warna memungkinkan untuk membuat citra baru dengan kombinasi warna yang dikustomisasi atau untuk menganalisis interaksi antara kanal warna yang berbeda.

4. Konversi ke Grayscale dan Thresholding:

Dalam kode program, terdapat proses konversi citra ke grayscale (keabuan) menggunakan fungsi cv2.cvtColor() dengan mode cv2.COLOR_BGR2GRAY. Citra grayscale hanya memiliki satu kanal intensitas, yang mewakili kombinasi ketiga kanal warna (merah, hijau, dan biru) dengan bobot tertentu.

Selanjutnya, kode program menerapkan metode thresholding adaptif pada citra grayscale menggunakan fungsi cv2.threshold() dengan metode cv2.THRESH_BINARY dan cv2.THRESH_OTSU. Thresholding adalah proses mengonversi citra grayscale menjadi citra biner (hitam dan putih) dengan membandingkan nilai intensitas piksel dengan suatu nilai ambang batas (threshold). Metode Otsu digunakan untuk menentukan nilai ambang batas secara otomatis berdasarkan analisis histogram citra.

Thresholding berguna untuk memisahkan objek dari latar belakang, mempersiapkan citra untuk proses segmentasi atau deteksi tepi, dan memfasilitasi operasi pengolahan citra lanjutan.

5. Penyortiran dan Pencetakan Nilai Ambang Batas:

Pada bagian akhir kode program, nilai ambang batas (threshold) yang diperoleh dari proses thresholding untuk setiap kanal warna dan citra grayscale diurutkan dan dicetak. Pengurutan dilakukan berdasarkan nilai ambang batas, dari yang terkecil hingga terbesar.

Nilai ambang batas yang berbeda dapat memberikan informasi tentang karakteristik kontras dan distribusi intensitas piksel dalam citra. Dengan menyortir dan mencetak nilai ambang batas, pengguna dapat menganalisis dan membandingkan tingkat kontras dan distribusi intensitas pada citra atau kanal warna yang berbeda.

6. Operasi Bitwise NOT (Invert Citra):

Pada bagian akhir kode program, terdapat operasi bitwise NOT yang diterapkan pada citra biner hasil dari proses thresholding menggunakan fungsi cv2.bitwise_not(). Operasi ini menghasilkan citra yang merupakan kebalikan (invers) dari citra input, di mana piksel hitam menjadi putih, dan piksel putih menjadi hitam.

Operasi invert citra dapat digunakan untuk mempersiapkan citra untuk proses pengolahan lanjutan, seperti deteksi objek atau analisis pola. Selain itu, citra yang diinvers juga sering digunakan untuk memvisualisasikan hasil dari operasi pengolahan citra tertentu, seperti deteksi tepi atau segmentasi objek.
