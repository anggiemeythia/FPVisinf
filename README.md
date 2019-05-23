## Data Penduduk Keluarga Berpenghasilan Rendah
### Data milik Pemkot Surabaya

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

### Creator
- Gamal Akbar Adzanni
- Anggie Meythia
- Muhammad Khotib

### Dependencies
- pandas
- matplotlib.pyplot
- numpy
