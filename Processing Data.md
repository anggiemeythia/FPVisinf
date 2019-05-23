
# Pengolahan Data

##### Kelompok : Anggie Meythia, Muhamad Khotib, Gamal Akbar

Dataset yang digunakan adalah data penduduk keluarga yang berpenghasilan rendah antara usia 15 – 45 tahun 
di seluruh kota Surabaya. Data terdiri dari 6 kolom yaitu NIK, tanggal lahir, jenis kelamin, deskripsi pekerjaan, 
pendidikan, dan hubungan keluarga.Baris dari dataset tersebut adalah sebanyak 386507. 


```python
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
```


```python
df = pd.read_csv('E:/Materi Kuliah/Visualisasi Informasi/FP/data_penghasilanrendah.csv')
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NIK</th>
      <th>tgl_lhr</th>
      <th>jenis_klmn</th>
      <th>pkrjn_descrip</th>
      <th>pendidikan_descrip</th>
      <th>hubkel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.578020e+15</td>
      <td>7/27/1978 00:00:00</td>
      <td>PEREMPUAN</td>
      <td>KARYAWAN HONORER</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.578010e+15</td>
      <td>4/25/1988 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.578210e+15</td>
      <td>3/16/1977 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>BURUH HARIAN LEPAS</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.578010e+15</td>
      <td>12/19/1995 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.578020e+15</td>
      <td>2/27/1979 00:00:00</td>
      <td>PEREMPUAN</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.201050e+15</td>
      <td>8/15/1984 00:00:00</td>
      <td>PEREMPUAN</td>
      <td>WIRASWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.578010e+15</td>
      <td>11-04-78 0:00</td>
      <td>LAKI-LAKI</td>
      <td>WIRASWASTA</td>
      <td>DIPLOMA IV/STRATA I</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3.316150e+15</td>
      <td>8/25/1998 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3.578010e+15</td>
      <td>3/26/2004 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>BELUM TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.578010e+15</td>
      <td>6/13/1975 00:00:00</td>
      <td>LAKI-LAKI</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    NIK                   float64
    tgl_lhr                object
    jenis_klmn             object
    pkrjn_descrip          object
    pendidikan_descrip     object
    hubkel                 object
    dtype: object



## Mengubah menjadi format tanggal

Memastikan tgl_lahir memiliki format waktu yang sama sehingga dapat dilakukan perhitungan umur 


```python
#convert to date
df['tgl_lhr'] = pd.to_datetime(df['tgl_lhr'])
```


```python
df[:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NIK</th>
      <th>tgl_lhr</th>
      <th>jenis_klmn</th>
      <th>pkrjn_descrip</th>
      <th>pendidikan_descrip</th>
      <th>hubkel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.578020e+15</td>
      <td>1978-07-27</td>
      <td>PEREMPUAN</td>
      <td>KARYAWAN HONORER</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.578010e+15</td>
      <td>1988-04-25</td>
      <td>LAKI-LAKI</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.578210e+15</td>
      <td>1977-03-16</td>
      <td>LAKI-LAKI</td>
      <td>BURUH HARIAN LEPAS</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.578010e+15</td>
      <td>1995-12-19</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.578020e+15</td>
      <td>1979-02-27</td>
      <td>PEREMPUAN</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.201050e+15</td>
      <td>1984-08-15</td>
      <td>PEREMPUAN</td>
      <td>WIRASWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>ISTRI</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.578010e+15</td>
      <td>1978-11-04</td>
      <td>LAKI-LAKI</td>
      <td>WIRASWASTA</td>
      <td>DIPLOMA IV/STRATA I</td>
      <td>KEPALA KELUARGA</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3.316150e+15</td>
      <td>1998-08-25</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3.578010e+15</td>
      <td>2004-03-26</td>
      <td>LAKI-LAKI</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>BELUM TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.578010e+15</td>
      <td>1975-06-13</td>
      <td>LAKI-LAKI</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[['pkrjn_descrip' ,'pendidikan_descrip','hubkel']] = df[['pkrjn_descrip' ,'pendidikan_descrip','hubkel']].astype(str)

```


```python
df.dtypes
```




    NIK                          float64
    tgl_lhr               datetime64[ns]
    jenis_klmn                    object
    pkrjn_descrip                 object
    pendidikan_descrip            object
    hubkel                        object
    dtype: object



## Pengkodean Jenis Kelamin menjadi L dan P

Memudahkan pengolahan data dengan mengubah ke data kategorikal L dan P


```python
#Convert to L/P
df1 = df
df1['jenis_klmn'] = df1['jenis_klmn'].apply(lambda x: 'L' if x == 'LAKI-LAKI' else 'P')
```

## Pengecekan Nilai Kosong

Sebelum memulai pengolahan data, terlebih dahulu harus dipastikan bahwa 
dataset yang digunakan tidak terdapat nilai yang kosong. 
Pada pengecekan yang dilakuakan, tidak ditemukan baris/sel yang kosong.


```python
df1.isnull().values.any()
```




    False



## Penentuan Kecamatan Berdasarkan NIK

Penentuan Kecamatan didasarkan dengan NIK yang dimiliki setiap masyarakat, 4 angka pertama NIK merupakan kode propinsi dan kota
lalu 2 angka yang mengikutinya merupakan kode kecamata. dengan data dari kemendagri, maka dilakukan pencocokan
kode kecamatan


```python
df3 = df['NIK']
df3 = df3.astype(str)
df3.dtypes

# df3.str[:6]
```




    dtype('O')




```python
listkec = {'357801':'Karang Pilang', '357802':'Wonocolo', '357803':'Rungkut', '357804':'Wonokromo', '357805':'Tegalsari', '357806':'Sawahan', '357807':'Genteng',
              '357808':'Gubeng', '357809':'Sukolilo', '357810':'Tambaksari', '357811':'Simokerto', '357812':'Pabean Cantian', '357813':'Bubutan', 
               '357814':'Tandes', '357815':'Krembangan', '357816':'Semampir', '357817':'Kenjeran', '357818':'Lakarsantri', '357819':'Benowo', '357820':'Wiyung',
               '357821':'Dukuh Pakis', '357822':'Gayungan', '357823':'Jambangan', '357824':'Tenggilis Mejoyo', '357825':'Gunung Anyar', '357826':'Mulyorejo',
               '357827':'Sukomanunggal', '357828':'Asem Rowo', '357829':'Bulak', '357830':'Pakal', '357831':'Sambikerep'
                }
# print (listkec.get('357801'))

tempkecamatan = df3.str[:6].apply(lambda x : listkec.get(x))

df['kecamatan'] = tempkecamatan
df[:10]


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NIK</th>
      <th>tgl_lhr</th>
      <th>jenis_klmn</th>
      <th>pkrjn_descrip</th>
      <th>pendidikan_descrip</th>
      <th>hubkel</th>
      <th>kecamatan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.578020e+15</td>
      <td>1978-07-27</td>
      <td>P</td>
      <td>KARYAWAN HONORER</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>Wonocolo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.578010e+15</td>
      <td>1988-04-25</td>
      <td>L</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.578210e+15</td>
      <td>1977-03-16</td>
      <td>L</td>
      <td>BURUH HARIAN LEPAS</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Dukuh Pakis</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.578010e+15</td>
      <td>1995-12-19</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ANAK</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.578020e+15</td>
      <td>1979-02-27</td>
      <td>P</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>Wonocolo</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.201050e+15</td>
      <td>1984-08-15</td>
      <td>P</td>
      <td>WIRASWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>None</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.578010e+15</td>
      <td>1978-11-04</td>
      <td>L</td>
      <td>WIRASWASTA</td>
      <td>DIPLOMA IV/STRATA I</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3.316150e+15</td>
      <td>1998-08-25</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3.578010e+15</td>
      <td>2004-03-26</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>BELUM TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.578010e+15</td>
      <td>1975-06-13</td>
      <td>L</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
  </tbody>
</table>
</div>



## Simpan File CSV 


```python
df.to_csv('data.csv')
```
