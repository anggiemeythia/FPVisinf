
# Visualisasi Data Gakin

----------------------------------------------------------------------------------------------------------------------------

### Gamal Akbar

a.	Jumlah keluarga yang dihitung berdasarkan kepala keluarga yang ada

b.	Jenis pekerjaan berdasarkan jenis kelamin

c.	Jumlah orang yang tidak tamat sekolah berdasarkan jenis kelamin

d.	Rata rata usia anak dalam kolom ‘hubkel’

e.	Jenis pekerjaan berdasarkan istri dalam kolom ‘hubkel’

f.	Rentang usia berdasarkan kepala keluarga

g.	Jenis pekerjaan berdasarkan warga lulusan SLTA/SEDERAJAT

h.	Jumlah warga yang berdasarkan lulusan perguruan tinggi

i.	Jumlah wiraswasta berdasarkan jenis kelamin

j.	Tingkat Pendidikan pengangguran per kecamatan


```python
%matplotlib inline

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

#Plot
import plotly.plotly as py
import plotly.graph_objs as go

```


```python
df = pd.read_csv('data.csv')
df = df.drop(columns="in")
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
      <th>kecamatan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.578020e+15</td>
      <td>1978-07-27 00:00:00</td>
      <td>P</td>
      <td>KARYAWAN HONORER</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>Wonocolo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.578010e+15</td>
      <td>1988-04-25 00:00:00</td>
      <td>L</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.578210e+15</td>
      <td>1977-03-16 00:00:00</td>
      <td>L</td>
      <td>BURUH HARIAN LEPAS</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Dukuh Pakis</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.578010e+15</td>
      <td>1995-12-19 00:00:00</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ANAK</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.578020e+15</td>
      <td>1979-02-27 00:00:00</td>
      <td>P</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTA/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>Wonocolo</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.201050e+15</td>
      <td>1984-08-15 00:00:00</td>
      <td>P</td>
      <td>WIRASWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>ISTRI</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.578010e+15</td>
      <td>1978-11-04 00:00:00</td>
      <td>L</td>
      <td>WIRASWASTA</td>
      <td>DIPLOMA IV/STRATA I</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3.316150e+15</td>
      <td>1998-08-25 00:00:00</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3.578010e+15</td>
      <td>2004-03-26 00:00:00</td>
      <td>L</td>
      <td>PELAJAR/MAHASISWA</td>
      <td>BELUM TAMAT SD/SEDERAJAT</td>
      <td>ANAK</td>
      <td>Karang Pilang</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.578010e+15</td>
      <td>1975-06-13 00:00:00</td>
      <td>L</td>
      <td>KARYAWAN SWASTA</td>
      <td>SLTP/SEDERAJAT</td>
      <td>KEPALA KELUARGA</td>
      <td>Karang Pilang</td>
    </tr>
  </tbody>
</table>
</div>



### Jenis Kelamin per Kecamatan


```python
df.dropna(axis=0, how='all', inplace=True)
df_kec = df['kecamatan'].value_counts()
df_laki = df['kecamatan'].where(df['jenis_klmn']=="L").value_counts()
df_perem = df['kecamatan'].where(df['jenis_klmn']=="P").value_counts()

print(df_kec)

trace1 = go.Bar(
    x=df_laki.index,
    y=df_laki,
    name='Laki Laki'
)
trace2 = go.Bar(
    x=df_perem.index,
    y=df_perem,
    name='Perempuan'
)


data = [trace1, trace2]
layout = go.Layout(
    xaxis=dict(tickangle=-45),
    barmode='group',
    title = 'Jumlah L/P setiap kecamatan'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='group-bar')
```

    Semampir         29606
    Kenjeran         26735
    Tambaksari       23651
    Simokerto        23078
                     ...  
    Jambangan         4740
    Gunung Anyar      4639
    Gayungan          4360
    Karang Pilang     4066
    Name: kecamatan, Length: 31, dtype: int64
    




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/127.embed" height="525px" width="100%"></iframe>



### Jumlah keluarga yang dihitung berdasarkan kepala keluarga yang ada perkecamatan


```python
df_kec = df['kecamatan'].value_counts()
df_kepkel = df['kecamatan'].where(df['hubkel']=="KEPALA KELUARGA").value_counts()
df_kepkel
```




    Semampir            7415
    Tambaksari          6345
    Kenjeran            5063
    Sawahan             4700
                        ... 
    Jambangan           1121
    Tenggilis Mejoyo    1098
    Gunung Anyar         979
    Gayungan             871
    Name: kecamatan, Length: 31, dtype: int64




```python
trace0 = go.Bar(
    x= df_kepkel.index,
    y= df_kepkel,
    name='Keluarga',
    marker=dict(
        color='rgb(49,130,189)'
    )
)

data = [trace0]
layout = go.Layout(
    xaxis=dict(tickangle=-45),
    barmode='stack',
    title = 'Jumlah Keluarga Setiap Kecamatan'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='stack-bar')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/129.embed" height="525px" width="100%"></iframe>



### Jenis pekerjaan berdasarkan jenis kelamin per kecamatan


```python
from plotly import tools
import plotly.plotly as py
import plotly.graph_objs as go


df_kec = df['kecamatan'].value_counts()



filterL = df['jenis_klmn']=="L"
filterP = df['jenis_klmn']=="P"
filterWon = df['kecamatan'] =='Wonocolo'
filterSem = df['kecamatan'] =='Semampir'
filterKen = df['kecamatan'] =='Kenjeran'
filterTam = df['kecamatan'] =='Tambaksari'
filterSim = df['kecamatan'] =='Simokerto'
filterSaw = df['kecamatan'] =='Sawahan'


#Kec 1
fil_kec_L = df[filterL & filterWon][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P = df[filterP & filterWon][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]

#Kec 2
fil_kec_L_1 = df[filterL & filterSem][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P_1 = df[filterP & filterSem][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
#Kec 3
fil_kec_L_2 = df[filterL & filterKen][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P_2 = df[filterP & filterKen][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
#Kec 4
fil_kec_L_3 = df[filterL & filterTam][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P_3 = df[filterP & filterTam][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
#Kec 5
fil_kec_L_4 = df[filterL & filterSim][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P_4 = df[filterP & filterSim][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
#Kec 6
fil_kec_L_5 = df[filterL & filterSaw][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]
fil_kec_P_5 = df[filterP & filterSaw][['jenis_klmn','pkrjn_descrip']].groupby('pkrjn_descrip').size().sort_values(ascending=False)[:5]



trace1 = go.Bar(
    x=fil_kec_L.index,
    y=fil_kec_L,
    name='Laki Laki'
)
trace2 = go.Bar(
    x=fil_kec_P.index,
    y=fil_kec_P,
    name='Perempuan'
)

trace3 = go.Bar(
    x=fil_kec_L_1.index,
    y=fil_kec_L_1,
    name='Laki Laki'
)
trace4 = go.Bar(
    x=fil_kec_P_1.index,
    y=fil_kec_P_1,
    name='Perempuan'
)

trace5 = go.Bar(
    x=fil_kec_L_2.index,
    y=fil_kec_L_2,
    name='Laki Laki'
)
trace6 = go.Bar(
    x=fil_kec_P_2.index,
    y=fil_kec_P_2,
    name='Perempuan'
)

trace7 = go.Bar(
    x=fil_kec_L_3.index,
    y=fil_kec_L_3,
    name='Laki Laki'
)
trace8 = go.Bar(
    x=fil_kec_P_3.index,
    y=fil_kec_P_3,
    name='Perempuan'
)

trace9 = go.Bar(
    x=fil_kec_L_4.index,
    y=fil_kec_L_4,
    name='Laki Laki'
)
trace10 = go.Bar(
    x=fil_kec_P_4.index,
    y=fil_kec_P_4,
    name='Perempuan'
)

trace11 = go.Bar(
    x=fil_kec_L_5.index,
    y=fil_kec_L_5,
    name='Laki Laki'
)
trace12 = go.Bar(
    x=fil_kec_P_5.index,
    y=fil_kec_P_5,
    name='Perempuan'
)




fig = tools.make_subplots(rows=3, cols=2,subplot_titles=('Wonocolo','Semampir','Kenjeran','Tambaksari','Simokerto',
                                                        'Sawahan'))
fig.append_trace(trace1, 1, 1)
fig.append_trace(trace2, 1, 1)
fig.append_trace(trace3, 1, 2)
fig.append_trace(trace4, 1, 2)
fig.append_trace(trace5, 2, 1)
fig.append_trace(trace6, 2, 1)
fig.append_trace(trace7, 2, 2)
fig.append_trace(trace8, 2, 2)
fig.append_trace(trace9, 3, 1)
fig.append_trace(trace10, 3, 1)
fig.append_trace(trace11, 3, 2)
fig.append_trace(trace12, 3, 2)

fig['layout'].update(height=1000, width=1000, title='Pekerjaan berdasarkan jenis kelamin per kecamatan')
py.iplot(fig, filename='custom binning')
```

    This is the format of your plot grid:
    [ (1,1) x1,y1 ]  [ (1,2) x2,y2 ]
    [ (2,1) x3,y3 ]  [ (2,2) x4,y4 ]
    [ (3,1) x5,y5 ]  [ (3,2) x6,y6 ]
    
    




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/131.embed" height="1000px" width="1000px"></iframe>



## Jumlah orang yang tidak tamat sekolah berdasarkan jenis kelamin


```python
df_tdkTamat = df['pendidikan_descrip'].str.contains('BELUM TAMAT SD')
filterL = df['jenis_klmn'] == "L"
filterP = df['jenis_klmn'] == "P"

df_k_L = df[df_tdkTamat & filterL]
df_k_P = df[df_tdkTamat & filterP]


jml_L = df_k_L.groupby('kecamatan').count().jenis_klmn
jml_P = df_k_P.groupby('kecamatan').count().jenis_klmn


trace1 = go.Bar(
    x=jml_L.index,
    y=jml_L,
    name='Laki Laki'
)
trace2 = go.Bar(
    x=jml_P.index,
    y=jml_P,
    name='Perempuan'
)


data = [trace1, trace2]
layout = go.Layout(
    barmode='stack',
    title = 'Jumlah orang yang tidak tamat sekolah berdasarkan jenis kelamin per kecamatan'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='stacked-bar')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/133.embed" height="525px" width="100%"></iframe>



## Rata rata usia anak per kecamatan


```python
df_anak = df['hubkel']=="ANAK"

df2 = df[df_anak]
df_date = pd.to_datetime(df2['tgl_lhr'])


now = pd.Timestamp('now')
df2['Usia'] = (now - df_date).astype('<m8[Y]')

df3 = df2[['Usia', 'kecamatan']]
df3.dropna()

dfWon = df3.where(df3['kecamatan'] == 'Wonocolo').dropna()
dfSem = df3.where(df3['kecamatan'] == 'Semampir').dropna()
dfKen = df3.where(df3['kecamatan'] == 'Kenjeran').dropna()
dfTam = df3.where(df3['kecamatan'] == 'Tambaksari').dropna()
dfSim = df3.where(df3['kecamatan'] == 'Simokerto').dropna()
dfSaw = df3.where(df3['kecamatan'] == 'Sawahan').dropna()

```

    C:\Users\Gamal\AppData\Local\conda\conda\envs\MLROOT\lib\site-packages\ipykernel_launcher.py:8: SettingWithCopyWarning:
    
    
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    
    


```python
# x = df2['kecamatan']

trace1 = go.Box(
    x = dfWon['kecamatan'],
    y = dfWon['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)
trace2 = go.Box(
    x = dfSem['kecamatan'],
    y = dfSem['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)
trace3 = go.Box(
    x = dfKen['kecamatan'],
    y = dfKen['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)
trace4 = go.Box(
    x = dfTam['kecamatan'],
    y = dfTam['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)
trace5 = go.Box(
    x = dfSim['kecamatan'],
    y = dfSim['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)
trace6 = go.Box(
    x = dfSaw['kecamatan'],
    y = dfSaw['Usia'],
    name = "Suspected Outliers",
    boxpoints = 'suspectedoutliers',
    marker = dict(
        color = 'rgb(8,81,156)',
        outliercolor = 'rgba(219, 64, 82, 0.6)',
        line = dict(
            outliercolor = 'rgba(219, 64, 82, 0.6)',
            outlierwidth = 2)),
    line = dict(
        color = 'rgb(8,81,156)')
)


data = [trace1,trace2, trace3, trace4, trace5, trace6]

layout = go.Layout(
    title = "Box Plot Rata rata umur anak 6 kecamatan"
)

fig = go.Figure(data=data,layout=layout)
py.iplot(fig,)
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/135.embed" height="525px" width="100%"></iframe>



### Jenis pekerjaan Istri per kecamatan


```python
df_istri = df['hubkel'] == "ISTRI"
df_kec = df['kecamatan'].value_counts()
df_pkr = df['pkrjn_descrip'].value_counts()
df_kec1 = df[df_istri].groupby('pkrjn_descrip').count().sort_values(ascending=False, by='NIK')[:5]

df_kec_art = df['kecamatan'].where(df['pkrjn_descrip'] == 'MENGURUS RUMAH TANGGA').value_counts()
df_kec_swt = df['kecamatan'].where(df['pkrjn_descrip'] == 'KARYAWAN SWASTA').value_counts()
df_kec_wira = df['kecamatan'].where(df['pkrjn_descrip'] == 'WIRASWASTA').value_counts()
df_kec_tidak = df['kecamatan'].where(df['pkrjn_descrip'] == 'BELUM/TIDAK BEKERJA').value_counts()

df_kec_total = pd.concat([df_kec_art, df_kec_swt, df_kec_wira, df_kec_tidak], axis=1, sort=True)
df_kec_total.columns = ['Ibu rumah Tangga', 'Swasta', 'Wiraswasta', 'Tidak bekerja']
df_kec_total.plot(kind="bar", figsize=[50,50], fontsize=45, legend="True")

```




    <matplotlib.axes._subplots.AxesSubplot at 0x2687979d5c0>




![png](output_19_1.png)


### Rentang usia Kepala keluarga


```python
import datetime as DT
import numpy as np

df_kp = df['hubkel'] == "KEPALA KELUARGA"
# df1 = df[df_kp].copy()

df1['tgl_lhr'] = pd.to_datetime(df1['tgl_lhr'])
# df1['tgl_lhr'].apply('{:06}'.format)



now = pd.Timestamp('now')
df1['umur'] = (now - df1['tgl_lhr']).astype('<m8[Y]')

df_umr_1 = df1['umur']
df_umr = df1['umur'].where(df_kp).value_counts()
df_umr_total = pd.concat([df_umr_1, df_umr], axis=1, sort=True)
df_umr_total.columns = ['Usia', 'Jumlah']
df_umr_total.dropna()
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
      <th>Usia</th>
      <th>Jumlah</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17.0</th>
      <td>31.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>24.0</th>
      <td>34.0</td>
      <td>827.0</td>
    </tr>
    <tr>
      <th>29.0</th>
      <td>33.0</td>
      <td>2313.0</td>
    </tr>
    <tr>
      <th>32.0</th>
      <td>43.0</td>
      <td>3160.0</td>
    </tr>
    <tr>
      <th>36.0</th>
      <td>34.0</td>
      <td>5029.0</td>
    </tr>
    <tr>
      <th>38.0</th>
      <td>38.0</td>
      <td>5238.0</td>
    </tr>
    <tr>
      <th>39.0</th>
      <td>41.0</td>
      <td>5310.0</td>
    </tr>
    <tr>
      <th>41.0</th>
      <td>25.0</td>
      <td>5539.0</td>
    </tr>
    <tr>
      <th>43.0</th>
      <td>27.0</td>
      <td>5818.0</td>
    </tr>
    <tr>
      <th>44.0</th>
      <td>44.0</td>
      <td>5925.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import plotly.plotly as py
import plotly.graph_objs as go


data = [
  go.Histogram(
    y = df_umr_total['Jumlah'],
    x = df_umr_total['Usia'],
  )
]




layout = go.Layout(
    title='Persebaran Umur',
    xaxis=dict(
        title='Umur'
    ),
    yaxis=dict(
        title='Jumlah'
    ),
    bargap=0.2,
    bargroupgap=0.1,
    shapes= [{'line': {'color': 'red', 'dash': 'solid', 'width': 3},
    'type': 'line',
    'x0': df_umr_total['Usia'].mean(),
    'x1': df_umr_total['Usia'].mean(),
    'xref': 'x',
    'y0': -0.1,
    'y1': 1,
    'yref': 'paper'}],
     annotations=[
        dict(
            x=df_umr_total['Usia'].mean(),
            y=1,
            xref='x',
            yref='y',
            text="Mean a = {:,.0f}".format(df_umr_total['Usia'].mean()),
            showarrow=True,
            arrowhead=7,
            ax=1,
            ay=1,
#             axref='pixel',
#             ayref='pixel'
        )]
)
fig = go.Figure(data=data, layout=layout)
py.iplot(fig)
```

    C:\Users\Gamal\AppData\Local\conda\conda\envs\MLROOT\lib\site-packages\plotly\plotly\plotly.py:230: UserWarning:
    
    Woah there! Look at all those points! Due to browser limitations, the Plotly SVG drawing functions have a hard time graphing more than 500k data points for line charts, or 40k points for other types of charts. Here are some suggestions:
    (1) Use the `plotly.graph_objs.Scattergl` trace object to generate a WebGl graph.
    (2) Trying using the image API to return an image instead of a graph URL
    (3) Use matplotlib
    (4) See if you can create your visualization with fewer data points
    
    If the visualization you're using aggregates points (e.g., box plot, histogram, etc.) you can disregard this warning.
    
    




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/137.embed" height="525px" width="100%"></iframe>



### Jenis pekerjaan berdasarkan warga lulusan SLTA/SEDERAJAT  setiap Kecamatan


```python
df_slta = df['pendidikan_descrip'] == "SLTA/SEDERAJAT"
dfx = df[df_slta].copy()
dfx_kec = dfx['kecamatan'].value_counts()
dfc = dfx['pkrjn_descrip'].value_counts()

dfe = dfx[['kecamatan', 'pkrjn_descrip']]
sa = dfe[:250].dropna()
sa
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
      <th>kecamatan</th>
      <th>pkrjn_descrip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wonocolo</td>
      <td>KARYAWAN HONORER</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Karang Pilang</td>
      <td>KARYAWAN SWASTA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Karang Pilang</td>
      <td>PELAJAR/MAHASISWA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonocolo</td>
      <td>KARYAWAN SWASTA</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>578</th>
      <td>Karang Pilang</td>
      <td>KARYAWAN SWASTA</td>
    </tr>
    <tr>
      <th>579</th>
      <td>Karang Pilang</td>
      <td>KARYAWAN SWASTA</td>
    </tr>
    <tr>
      <th>580</th>
      <td>Karang Pilang</td>
      <td>KARYAWAN SWASTA</td>
    </tr>
    <tr>
      <th>582</th>
      <td>Wonocolo</td>
      <td>MENGURUS RUMAH TANGGA</td>
    </tr>
  </tbody>
</table>
<p>242 rows × 2 columns</p>
</div>




```python
import pySankey
import matplotlib.pyplot as plt


pd.options.display.max_rows=8
%matplotlib inline
colorDict = {
    "Gayungan" : "#800000","Wiyung" : "#B22222",
    "Kenjeran" : "#FF4500",
    "Lakarsantri" : "#FFD700",
    "Sukomanunggal" : "#DAA520","Jambangan": "#F0E68C",
    "Gunung Anyar": "#808000",
    "Wonokromo" : "#6B8E23","Sawahan": "#ADFF2F",
    "Semampir": "#228B22",
    "KARYAWAN HONORER": "#bbdefb",
    "KARYAWAN SWASTA": "#bb8fce",
    "PELAJAR/MAHASISWA": "#2b49b6",
    "MENGURUS RUMAH TANGGA": "#784212",
    "BELUM/TIDAK BEKERJA": "#aed6f1",
    "BURUH HARIAN LEPAS": "#f4d03f",
    "WIRASWASTA": "#039be5",
    "TENTARA NASIONAL INDONESIA (TNI)": "#4a235a",
    "GURU": "#29b6f6","PEDAGANG": "#d81b60",
    "PERDAGANGAN": "#ff5722",
    "SOPIR": "#9ccc65",
    "KEPOLISIAN RI (POLRI)": "#b71c1c",    
    "Wonocolo" : "#6633CC",
    "Karang Pilang" : "#00CC00",
    "Dukuh Pakis": "#0d47a1",
    "Tegalsari": "#ffab91",
    "Tenggilis Mejoyo": "#c5cae9"
}

# actual call is left as an exercice to the reader but it could be something like
sankey.sankey(left=sa['kecamatan'], right=sa['pkrjn_descrip'],
              aspect=20, colorDict=colorDict, fontsize=10,
              figure_name="Kecamatan")
```


![png](output_25_0.png)


### Jumlah warga yang berdasarkan lulusan perguruan tinggi


```python
df_per = df['pendidikan_descrip'] == "DIPLOMA IV/STRATA I"

# dfpr = df[df_per].copy()
df_kec = df['kecamatan'].where(df_per).value_counts()
df_kec.plot(kind="bar", figsize=[10,10], fontsize=15);
```


![png](output_27_0.png)


### Jumlah wiraswasta berdasarkan jenis kelamin


```python
df_wir = df['pkrjn_descrip'] == "WIRASWASTA"
dfm = df[df_wir]
df_kec_l = dfm['kecamatan'].where(dfm['jenis_klmn'] == "L").value_counts()
df_kec_p =  dfm['kecamatan'].where(dfm['jenis_klmn'] == "P").value_counts()
```


```python
trace1 = go.Bar(
    x=df_kec_l.index,
    y=df_kec_l,
    name='Laki Laki'
)
trace2 = go.Bar(
    x=df_kec_p.index,
    y=df_kec_p,
    name='Perempuan'
)


data = [trace1, trace2]
layout = go.Layout(
    xaxis=dict(tickangle=-45),
    barmode='group',
    title = 'Jumlah Wirausaha L/P setiap kecamatan'
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='gbar')
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/139.embed" height="525px" width="100%"></iframe>



### Tingkat Pendidikan pengangguran per kecamatan


```python
ds = df['pkrjn_descrip'] == "BELUM/TIDAK BEKERJA"
dd = df[ds]
df_kc = dd['kecamatan'].value_counts()


def countid(df):
    count = 0
    for i in df:
        count += i
    return count
all_df = countid(df_kc)
ndf = df_kc.apply(lambda x: x/all_df)


ndf.plot(kind="area",figsize=[10,10])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x268894e3940>




![png](output_32_1.png)


-----------------------------------------------------------------------------------------------------------------------------

## Anggie Meythia

a.	Jumlah pekerja yang tidak tamat sekolah berdasarkan gender

b.	Jumlah pekerja yang berusia diatas usia kerja (usia harus pensiun 45 tahun) berdasarkan gender

c.	Jumlah anak dalam kolom ‘hubkel’ yang tidak sekolah berdasarkan gender

d.	Rata-rata usia pekerja berdasarkan gender

e.	Rata-rata usia pengangguran berdasarkan gender

f.	Rata-rata usia kepala keluarga dalam kolom ‘hubkel’

g.	Perbandingan yang bekerja dan tidak bekerja berdasarkan gender

h.	Perbandingan yang pendidikan terakhirnya SD/SLTP/SLTA dan Diploma/Sarjana berdasarkan gender 

i.	Perbandingan perempuan berusia diatas 18 tahun yang tidak bekerja atau menjadi ibu rumah tangga dan bekerja

j.	Jenis pekerjaan terbanyak yang dimiliki secara general


### Jumlah pekerja yang tidak tamat sekolah berdasarkan gender


```python
df_peng = df['pendidikan_descrip'] == "BELUM TAMAT SD/SEDERAJAT"
df1 = df[df_peng].copy()

df1_l = df1['kecamatan'].where(df1['jenis_klmn'] == "L").value_counts()
df1_p = df1['kecamatan'].where(df1['jenis_klmn'] == "L").value_counts()
df1_l
```




    Semampir            2501
    Simokerto           1716
    Tambaksari          1203
    Kenjeran            1177
                        ... 
    Tenggilis Mejoyo     322
    Gunung Anyar         306
    Asem Rowo            264
    Gayungan             256
    Name: kecamatan, Length: 31, dtype: int64




```python
import plotly.plotly as py
import plotly.graph_objs as go

import numpy as np


y = list(range(0, 400, 10))

layout = go.Layout(yaxis=go.layout.YAxis(title='Kecamatan'),
                   xaxis=go.layout.XAxis(
                       range=[-2600, 2600],
                       tickvals=[-2550, -1700, -1000, -500, 0, 500, 1000, 1700, 2550],
                       ticktext=[2550, 1700, 1000, 500, 0, 500, 1000, 1700, 2550],
                       title='Jumlah Pengangguran'),
                   barmode='overlay',
                   bargap=0.1)

data = [go.Bar(y=y,
               x=df1_l,
               orientation='h',
               name='Pria',
               hoverinfo='x',
               marker=dict(color='powderblue')
               ),
        go.Bar(y=y,
               x=-df1_p,
               orientation='h',
               name='Wanita',
               text=-1 * df1_p.astype('int'),
               hoverinfo='text',
               marker=dict(color='seagreen')
               )]

py.iplot(dict(data=data, layout=layout))
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/121.embed" height="525px" width="100%"></iframe>



### Jumlah pekerja yang berusia diatas usia kerja (usia harus pensiun 45 tahun) berdasarkan gender


```python
import datetime as DT
import numpy as np

dfv = df.copy()
# df_minage = 
dfv['tgl_lhr'] = pd.to_datetime(dfv['tgl_lhr'])




now = pd.Timestamp('now')
dfv['umur'] = (now - dfv['tgl_lhr']).astype('<m8[Y]')
df_minage = dfv['umur'] > 45
filtered = dfv[df_minage]
fl_l = filtered['umur'].where(filtered['jenis_klmn'] == "L").value_counts()
fl_p = filtered['umur'].where(filtered['jenis_klmn'] == "P").value_counts()
print(fl_l,fl_p)
```

    46.0    586
    Name: umur, dtype: int64 46.0    582
    Name: umur, dtype: int64
    


```python
trace1 = go.Bar(
    x=fl_l.index,
    y=fl_l,
    name='Laki Laki'
)
trace2 = go.Bar(
    x=fl_p.index,
    y=fl_p,
    name='Perempuan'
)


data = [trace1, trace2]
layout = go.Layout(
    xaxis=dict(tickangle=-45),
    barmode='group',
    title = 'Jumlah Pekerja yang mendekati pensiun',
)

fig = go.Figure(data=data, layout=layout)
py.iplot(fig, filename='group-bar1')
```

    C:\Users\Gamal\AppData\Local\conda\conda\envs\MLROOT\lib\site-packages\IPython\core\display.py:689: UserWarning:
    
    Consider using IPython.display.IFrame instead
    
    




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~azzamour/123.embed" height="525px" width="100%"></iframe>



### Jumlah anak  yang tidak sekolah berdasarkan gender


```python
df_anak = df['hubkel'] == "ANAK"
df_taktamat = df['pendidikan_descrip'] == "BELUM TAMAT SD/SEDERAJAT"
dfa = df[df_taktamat]
dfs = dfa[df_anak]
dfs_l = dfs['jenis_klmn'].value_counts()
dfs_l.plot(kind="bar")
```

    C:\Users\Gamal\AppData\Local\conda\conda\envs\MLROOT\lib\site-packages\ipykernel_launcher.py:4: UserWarning:
    
    Boolean Series key will be reindexed to match DataFrame index.
    
    




    <matplotlib.axes._subplots.AxesSubplot at 0x2685d47b3c8>




![png](output_43_2.png)


### Rata-rata usia pekerja berdasarkan gender


```python
dfv = df.copy()
dfv['tgl_lhr'] = pd.to_datetime(dfv['tgl_lhr'])

now = pd.Timestamp('now')
dfv['umur'] = (now - dfv['tgl_lhr']).astype('<m8[Y]')

dfv = dfv.groupby('jenis_klmn').mean().umur
dfv
```




    jenis_klmn
    L    29.334499
    P    30.020954
    Name: umur, dtype: float64




```python
dfv.plot(kind="bar")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2685ebd2828>




![png](output_46_1.png)


### Rata-rata usia pengangguran berdasarkan gender


```python
dfr = df.copy()
dfr['tgl_lhr'] = pd.to_datetime(dfr['tgl_lhr'])

now = pd.Timestamp('now')
dfr['umur'] = (now - dfr['tgl_lhr']).astype('<m8[Y]')

dfpp = dfr['pkrjn_descrip']=="BELUM/TIDAK BEKERJA"
dfr[dfpp]

dfm = dfr.groupby('jenis_klmn').mean().umur
dfm
```




    jenis_klmn
    L    29.334499
    P    30.020954
    Name: umur, dtype: float64




```python
dfm.plot(kind="bar")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2686748ad68>




![png](output_49_1.png)


### Rata-rata usia kepala keluarga dalam kolom ‘hubkel’


```python
dfo = df.copy()
dfo['tgl_lhr'] = pd.to_datetime(dfo['tgl_lhr'])

now = pd.Timestamp('now')
dfo['umur'] = (now - dfo['tgl_lhr']).astype('<m8[Y]')

dfio = dfo['hubkel']=="KEPALA KELUARGA"
dfo[dfio]

dfmi = dfr.groupby('jenis_klmn').mean().umur
dfmi
```




    jenis_klmn
    L    29.334499
    P    30.020954
    Name: umur, dtype: float64




```python
dfmi.plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2688f1a1860>




![png](output_52_1.png)


### Perbandingan yang bekerja dan tidak bekerja berdasarkan gender


```python
dfp = df.copy()
df_jen = dfp['jenis_klmn'].value_counts()
df_kerja = dfp['jenis_klmn'].where(dfp['pkrjn_descrip'] == "KARYAWAN SWASTA").value_counts()
df_tdkkerja =dfp['jenis_klmn'].where(dfp['pkrjn_descrip'] == "BELUM/TIDAK BEKERJA").value_counts()
df_tdkkerja
```




    L    28897
    P    25372
    Name: jenis_klmn, dtype: int64




```python
df_jen_total = pd.concat([df_kerja, df_tdkkerja], axis=1, sort=True)
df_jen_total.columns = ['Kerja', 'Belum bekerja']
df_jen_total.plot(kind="bar", figsize=[12,12], fontsize=12)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2685e4da4a8>




![png](output_55_1.png)


### Perbandingan yang pendidikan terakhirnya SD/SLTP/SLTA dan Diploma/Sarjana berdasarkan gender 


```python
dfq = df.copy()

df_SD = dfq['jenis_klmn'].where(dfp['pendidikan_descrip'] == "TAMAT SD/SEDERAJAT").value_counts()
df_SMP = dfq['jenis_klmn'].where(dfp['pendidikan_descrip'] == "SLTP/SEDERAJAT").value_counts()
df_SMA = dfq['jenis_klmn'].where(dfp['pendidikan_descrip'] == "SLTA/SEDERAJAT").value_counts()
df_Kuliah =dfq['jenis_klmn'].where(dfp['pendidikan_descrip'] == "DIPLOMA IV/STRATA I").value_counts()

df_Kuliah
```




    P    9294
    L    8084
    Name: jenis_klmn, dtype: int64




```python
df_pen_total = pd.concat([df_SD, df_SMP, df_SMA, df_Kuliah], axis=1, sort=True)
df_pen_total.columns = ['SD', 'SMP', 'SMA','KULIAH']
df_pen_total
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
      <th>SD</th>
      <th>SMP</th>
      <th>SMA</th>
      <th>KULIAH</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>L</th>
      <td>35802</td>
      <td>40177</td>
      <td>69755</td>
      <td>8084</td>
    </tr>
    <tr>
      <th>P</th>
      <td>38672</td>
      <td>39662</td>
      <td>67762</td>
      <td>9294</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pen_total.plot(kind="bar", figsize=[10,10])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x268891c38d0>




![png](output_59_1.png)


### Perbandingan perempuan berusia diatas 18 tahun yang tidak bekerja atau menjadi ibu rumah tangga dan bekerja


```python
dfw = df.copy()
dfw['tgl_lhr'] = pd.to_datetime(dfw['tgl_lhr'])

now = pd.Timestamp('now')
dfw['umur'] = (now - dfw['tgl_lhr']).astype('<m8[Y]')

dfwl = dfw['jenis_klmn'] == "P"
dw = dfw[dfwl]

ab_eigt = dfw['umur'] > 18
dw[ab_eigt]

#ibu rumah tangga
df_ibu = dw['jenis_klmn'].where(dw['pkrjn_descrip'] == "MENGURUS RUMAH TANGGA").value_counts()
df_ikerja = dw['jenis_klmn'].where(dw['pkrjn_descrip'] == "KARYAWAN SWASTA").value_counts()


df_ibu_total = pd.concat([df_ibu, df_ikerja], axis=1, sort=True)
df_ibu_total.columns = ['Ibu Rumah Tangga', 'Kerja']
df_ibu_total.plot(kind="bar", figsize=[10,10])
```

    C:\Users\Gamal\AppData\Local\conda\conda\envs\MLROOT\lib\site-packages\ipykernel_launcher.py:11: UserWarning:
    
    Boolean Series key will be reindexed to match DataFrame index.
    
    




    <matplotlib.axes._subplots.AxesSubplot at 0x2688a1bf438>




![png](output_61_2.png)


### Jenis pekerjaan terbanyak yang dimiliki secara general


```python
dcx = df['pkrjn_descrip'].value_counts()
dcx
```




    PELAJAR/MAHASISWA        121577
    KARYAWAN SWASTA          117623
    MENGURUS RUMAH TANGGA     70909
    BELUM/TIDAK BEKERJA       54269
                              ...  
    PENYIAR TELEVISI              1
    ANGGOTA DPRD PROP.            1
    IMAM MASJID                   1
    TUKANG CUKUR                  1
    Name: pkrjn_descrip, Length: 67, dtype: int64




```python
dcx[:4].plot(kind="bar")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2685eb88cc0>




![png](output_64_1.png)

