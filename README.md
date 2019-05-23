# Final Project Visualisasi Informasi
## Data Penduduk Keluarga Berpenghasilan Rendah
Data milik Pemkot Surabaya

### About Dataset
Dataset yang digunakan adalah data penduduk keluarga yang berpenghasilan rendah antara usia 15 – 45 tahun di seluruh kota Surabaya. Data terdiri dari 6 kolom yaitu NIK, tanggal lahir, jenis kelamin, deskripsi pekerjaan, pendidikan, dan hubungan keluarga. Baris dari dataset tersebut adalah sebanyak 386507.

Praprocessing data dilakukan untuk menambahkan atribut untuk menunjang keperluan visualisasi data. Sehingga, data mempunyai 8 atribut setelah dilakukan praprocessing data.

### Atribut Informasi
- NIK (float64): Berisi NIK dari penduduk Surabaya yang berpenghasilan rendah.
- tgl_lhr (object): Tanggal lahir penduduk.
- jenis_klmn (object): Jenis kelamin penduduk.
- pkrjn_descrip (object): Pekerjaan penduduk.
- pendidikan_descrip (object): Pendidikan terakhir penduduk.
- hubkel (object): Hubungan keluarga antar penduduk.

### Atribut Setelah Praprocessing
- kode_kec (object): Kode kecamatan penduduk.
- kec (object): Kecamatan tempat tinggal penduduk.
- umur (object): Umur penduduk.

### Tema Visualisasi
1. Keluarga Miskin
2. Pendidikan Terakhir Pekerja
3. Usia Pekerja.

### Creator
- Gamal Akbar Adzanni
- Anggie Meythia
- Muhammad Khotib

### Dependencies
- pandas
- matplotlib.pyplot
- numpy

## Preprocessing Data
#### 1. Mencari nilai yang kosong
Sebelum memulai pengolahan data, terlebih dahulu harus dipastikan bahwa dataset yang digunakan tidak terdapat nilai yang kosong. Pada pengecekan yang dilakukan, tidak ditemukan baris/sel yang kosong.
#### 2. Menstandarkan format dari tgl_lahir menjadi datetime
Langkah ini dilakukan karena terdapat beberapa baris yang berbeda format waktunya
#### 3. Mengubah kolom jenis kelamin menjadi L/P untuk memudahkan pengolahan data
Pada tahap ini, akan digunakan fungsi lambda dan kondisi if-else untuk mengubah ketika “LAKI-LAKI” menjadi L dan “PEREMPUAN” menjadi P.
#### 4. Menentukan kecamatan penduduk
Pada tahap ini, akan diambil 2 angka di urutan ke 5 dan 6 pada NIK untuk menentukan kecamatan dari masing-masing penduduk. Lalu dicocokkan dengan kode kecamatan yang didapat dari kemendagri dan akan ditulis nama kecamatannya.
#### 5. Menentukan umur penduduk
Pada tahap ini, akan mencari selisih dari waktu saat ini dengan tanggal lahir penduduk untuk mendapatkan umur masing-masing penduduk.

## Insight
### Anggie Meythia
1. Jumlah pekerja yang tidak tamat sekolah berdasarkan gender 
2. Jumlah pekerja yang berusia diatas usia kerja (usia harus pensiun 55 tahun) berdasarkan gender 
3. Jumlah anak dalam kolom ‘hubkel’ yang tidak sekolah berdasarkan gender 
4. Rata-rata usia pekerja berdasarkan gender 
5. Rata-rata usia pengangguran berdasarkan gender 
6. Rata-rata usia kepala keluarga dalam kolom ‘hubkel’ 
7. Perbandingan yang bekerja dan tidak bekerja berdasarkan gender 
8. Perbandingan yang pendidikan terakhirnya SD/SLTP/SLTA dan Diploma/Sarjana berdasarkan gender  
9. Perbandingan perempuan berusia diatas 18 tahun yang tidak bekerja atau menjadi ibu rumah tangga dan bekerja 
10. Jenis pekerjaan terbanyak yang dimiliki secara general 

### Muhammad Khotib
1. Rasio istri yang bekerja dan tidak bekerja 
2. Jumlah warga (bukan anak) yang tidak tamat SD 
3. Persentase istri yang tidak bekerja tetapi pendidikan SLTA 
4. Tingkat pendidikan paling dominan 
5. Persentase istri yang bekerja 
6. Persentase pendidikan kepala keluarga 
7. Jumlah anak dengan usia wajib sekolah (7-8 tahun) akan tetapi belum bersekolah 
8. Jumlah istri yang berusia dibawah 18 tahun  
9. Jumlah kepala keluarga yang tidak memiliki pekerjaan tetap (ex : Buruh Harian lepas, Karyawan honorer) 
10. Jumlah anak yang mampu berkuliah (Mahasiswa) 

### Gamal Akbar Adzanni
1. Jumlah keluarga yang dihitung berdasarkan kepala keluarga yang ada 
2. Jenis pekerjaan berdasarkan jenis kelamin 
3. Jumlah orang yang tidak tamat sekolah berdasarkan jenis kelamin 
4. Rata rata usia anak dalam kolom ‘hubkel’ 
5. Jenis pekerjaan berdasarkan istri dalam kolom ‘hubkel’ 
6. Rentang usia berdasarkan kepala keluarga 
7. Jenis pekerjaan berdasarkan warga lulusan SLTA/SEDERAJAT 
8. Jumlah warga yang memiliki pendidikan perkuliahan 
9. Jumlah wiraswasta berdasarkan jenis kelamin 
