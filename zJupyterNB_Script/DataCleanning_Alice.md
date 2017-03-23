

```python
%reset
```


```python
import os
import pandas as pd
```

# Part I: Data Clean


```python
os.chdir('/Users/yanlinli/Dropbox/141GroupPrj/OriginalData')
```


```python
cdl_data = pd.read_excel('cdl_ca_gw_basins.xlsx')
```


```python
cdl_data.shape
```




    (58865, 5)




```python
cdl_data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SMITH RIVER PLAIN</td>
      <td>NaN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>15879.436603</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SMITH RIVER PLAIN</td>
      <td>NaN</td>
      <td>2010</td>
      <td>Woody Wetlands</td>
      <td>4380.066439</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SMITH RIVER PLAIN</td>
      <td>NaN</td>
      <td>2010</td>
      <td>Developed/Open Space</td>
      <td>4112.525443</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SMITH RIVER PLAIN</td>
      <td>NaN</td>
      <td>2010</td>
      <td>Open Water</td>
      <td>3371.728220</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SMITH RIVER PLAIN</td>
      <td>NaN</td>
      <td>2010</td>
      <td>Evergreen Forest</td>
      <td>3339.480967</td>
    </tr>
  </tbody>
</table>
</div>




```python
import collections
collections.Counter(cdl_data.Basin_Name).most_common(3)
```




    [(u'SAN JOAQUIN VALLEY', 6633),
     (u'SACRAMENTO VALLEY', 5485),
     (u'SALINAS VALLEY', 2454)]




```python
cdl_data.ix[cdl_data.Basin_Name== u'SAN JOAQUIN VALLEY',].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32782</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
    </tr>
    <tr>
      <th>32783</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
    </tr>
    <tr>
      <th>32784</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
    </tr>
    <tr>
      <th>32785</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
    </tr>
    <tr>
      <th>32786</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
    </tr>
  </tbody>
</table>
</div>




```python
SanJQ = cdl_data.ix[cdl_data.Basin_Name== u'SAN JOAQUIN VALLEY',].reset_index(drop=True)
```


```python
SanJQ.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(SanJQ.Subbasin_N)
```




    Counter({u'CHOWCHILLA': 335,
             u'COSUMNES': 365,
             u'DELTA-MENDOTA': 442,
             u'EASTERN SAN JOAQUIN': 440,
             u'KAWEAH': 384,
             u'KERN COUNTY': 409,
             u'KETTLEMAN PLAIN': 210,
             u'KINGS': 434,
             u'MADERA': 379,
             u'MERCED': 388,
             u'MODESTO': 401,
             u'PLEASANT VALLEY': 211,
             u'TRACY': 408,
             u'TULARE LAKE': 377,
             u'TULE': 393,
             u'TURLOCK': 390,
             u'WESTSIDE': 391,
             u'WHITE WOLF': 276})




```python
subBasin_County_dict = {'CHOWCHILLA':"Madera","COSUMNES":"San Joaquin",
                    'DELTA-MENDOTA':'Stanislaus','EASTERN SAN JOAQUIN':'San Joaquin',
                   'KAWEAH':'Tulare','KERN COUNTY':'Kern','KETTLEMAN PLAIN':'Kings',
                    'KINGS':'Kings','MADERA':'Madera','MERCED':'Merced',
                    'MODESTO':'Stanislaus','PLEASANT VALLEY':'Fresno',
                    'TRACY':'San Joaquin','TULARE LAKE':'Kings','TULE':'Tulare',
                    'TURLOCK':'Stanislaus','WESTSIDE':'Fresno','WHITE WOLF':'Kern'}
```


```python
SanJQ["county"] = SanJQ["Subbasin_N"].map(subBasin_County_dict)
```


```python
SanJQ.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
dbl_crop = SanJQ.ix[SanJQ.cdl_class_name.str.startswith('Dbl'),]
```


```python
dbl_crop.shape
```




    (422, 6)




```python
type(dbl_crop)
```




    pandas.core.frame.DataFrame




```python
dbl_crop.iloc[0:3]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop Oats/Corn</td>
      <td>3479.367324</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>26</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop WinWht/Corn</td>
      <td>1360.166862</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>44</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop WinWht/Sorghum</td>
      <td>54.486737</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(dbl_crop.cdl_class_name)
```




    Counter({u'Dbl Crop Barley/Corn': 63,
             u'Dbl Crop Barley/Sorghum': 39,
             u'Dbl Crop Durum Wht/Sorghum': 6,
             u'Dbl Crop Lettuce/Cantaloupe': 2,
             u'Dbl Crop Lettuce/Cotton': 8,
             u'Dbl Crop Oats/Corn': 90,
             u'Dbl Crop WinWht/Corn': 97,
             u'Dbl Crop WinWht/Cotton': 37,
             u'Dbl Crop WinWht/Sorghum': 76,
             u'Dbl Crop WinWht/Soybeans': 4})




```python
dbl_crop.acres = dbl_crop.acres/2
```

    /Users/yanlinli/anaconda2/lib/python2.7/site-packages/pandas/core/generic.py:2773: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      self[name] = value



```python
dbl_crop.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop Oats/Corn</td>
      <td>1739.683662</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>26</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop WinWht/Corn</td>
      <td>680.083431</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>44</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Dbl Crop WinWht/Sorghum</td>
      <td>27.243368</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>89</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Dbl Crop Oats/Corn</td>
      <td>6434.994791</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>95</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Dbl Crop WinWht/Corn</td>
      <td>1725.339194</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
dcl_cdl_class_name_0=[]
dcl_cdl_class_name_1=[]
for i in (dbl_crop.cdl_class_name):
    dcl_cdl_class_name_0.append(str(i)[9:].split('/')[0])
    dcl_cdl_class_name_1.append(str(i)[9:].split('/')[1])
   
```


```python
dbl_crop.cdl_class_name= pd.DataFrame(dcl_cdl_class_name_0).values
dbl_crop_B  = dbl_crop.copy()
dbl_crop_B.cdl_class_name= pd.DataFrame(dcl_cdl_class_name_1).values
dbl_crop_B.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>1739.683662</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>26</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>680.083431</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>44</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Sorghum</td>
      <td>27.243368</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>89</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Corn</td>
      <td>6434.994791</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>95</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Corn</td>
      <td>1725.339194</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
dbl_crop.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Oats</td>
      <td>1739.683662</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>26</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>680.083431</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>44</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>27.243368</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>89</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Oats</td>
      <td>6434.994791</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>95</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>WinWht</td>
      <td>1725.339194</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(dbl_crop.cdl_class_name)
```




    Counter({'Barley': 102,
             'Durum Wht': 6,
             'Lettuce': 10,
             'Oats': 90,
             'WinWht': 214})




```python
#pd.DataFrame(dcl_cdl_class_name_0).values
type(pd.DataFrame(dcl_cdl_class_name_0).values)
pd.DataFrame(dcl_cdl_class_name_0).values.dtype
SanJQ.cdl_class_name.values.dtype
```




    dtype('O')




```python
double_full_df = pd.concat([dbl_crop, dbl_crop_B],ignore_index=True)
print double_full_df.shape
double_full_df.head()
```

    (844, 6)





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Oats</td>
      <td>1739.683662</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>680.083431</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>27.243368</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Oats</td>
      <td>6434.994791</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>WinWht</td>
      <td>1725.339194</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
SanJQ.ix[~SanJQ.cdl_class_name.str.startswith('Dbl'),].shape
```




    (6211, 6)




```python
SanJQ.shape
```




    (6633, 6)




```python
SanJQ.ix[SanJQ.cdl_class_name.str.startswith('Dbl'),].shape
```




    (422, 6)




```python
SanJQ.ix[~SanJQ.cdl_class_name.str.startswith('Dbl'),].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
double_full_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Oats</td>
      <td>1739.683662</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>680.083431</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>WinWht</td>
      <td>27.243368</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Oats</td>
      <td>6434.994791</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>WinWht</td>
      <td>1725.339194</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([SanJQ.ix[~SanJQ.cdl_class_name.str.startswith('Dbl'),], double_full_df],ignore_index=True).shape
```




    (7055, 6)




```python
6211+422*2
```




    7055




```python
SanJQ_single = pd.concat([SanJQ.ix[~SanJQ.cdl_class_name.str.startswith('Dbl'),], double_full_df],ignore_index=True)
```


```python
SanJQ_single.shape
```




    (7055, 6)




```python
SanJQ_single.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
      <td>San Joaquin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
      <td>San Joaquin</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(SanJQ_single.cdl_class_name)
type(SanJQ_single.cdl_class_name)
```




    pandas.core.series.Series




```python
len(SanJQ_single.cdl_class_name)
```




    7055




```python
SanJQ_single.ix[SanJQ_single.cdl_class_name =='Cantaloupe']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6833</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KINGS</td>
      <td>2012</td>
      <td>Cantaloupe</td>
      <td>1.111974</td>
      <td>Kings</td>
    </tr>
    <tr>
      <th>6862</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>WESTSIDE</td>
      <td>2012</td>
      <td>Cantaloupe</td>
      <td>131.880142</td>
      <td>Fresno</td>
    </tr>
  </tbody>
</table>
</div>




```python
SanJQ_single.set_value([6833,6862],'cdl_class_name',u'Cantaloupes')
SanJQ_single.iloc[[6833,6862],]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6833</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KINGS</td>
      <td>2012</td>
      <td>Cantaloupes</td>
      <td>1.111974</td>
      <td>Kings</td>
    </tr>
    <tr>
      <th>6862</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>WESTSIDE</td>
      <td>2012</td>
      <td>Cantaloupes</td>
      <td>131.880142</td>
      <td>Fresno</td>
    </tr>
  </tbody>
</table>
</div>




```python
#SanJQ_single.ix[SanJQ_single.cdl_class_name =='WinWht'] #Winter Wheat
#SanJQ_single.ix[SanJQ_single.cdl_class_name =='Durum Wht'] #Durum Wheat
```


```python
ind = SanJQ_single.ix[SanJQ_single.cdl_class_name =='WinWht'].index.values
```


```python
SanJQ_single.set_value(ind,'cdl_class_name',u'Winter Wheat')
SanJQ_single.ix[6212]
```




    Basin_Name         SAN JOAQUIN VALLEY
    Subbasin_N        EASTERN SAN JOAQUIN
    year                             2010
    cdl_class_name           Winter Wheat
    acres                         680.083
    county                    San Joaquin
    Name: 6212, dtype: object




```python
indDW = SanJQ_single.ix[SanJQ_single.cdl_class_name =='Durum Wht'].index.values #Durum Wheat
indDW
```




    array([6476, 6483, 6509, 6546, 6571, 6578])




```python
SanJQ_single.set_value(indDW,'cdl_class_name',u'Durum Wheat')
SanJQ_single.ix[indDW]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6476</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KAWEAH</td>
      <td>2013</td>
      <td>Durum Wheat</td>
      <td>0.555987</td>
      <td>Tulare</td>
    </tr>
    <tr>
      <th>6483</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KAWEAH</td>
      <td>2014</td>
      <td>Durum Wheat</td>
      <td>14.344467</td>
      <td>Tulare</td>
    </tr>
    <tr>
      <th>6509</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>TULARE LAKE</td>
      <td>2013</td>
      <td>Durum Wheat</td>
      <td>11.453334</td>
      <td>Kings</td>
    </tr>
    <tr>
      <th>6546</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>TULE</td>
      <td>2014</td>
      <td>Durum Wheat</td>
      <td>0.444790</td>
      <td>Tulare</td>
    </tr>
    <tr>
      <th>6571</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>2013</td>
      <td>Durum Wheat</td>
      <td>0.444790</td>
      <td>Kern</td>
    </tr>
    <tr>
      <th>6578</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>2014</td>
      <td>Durum Wheat</td>
      <td>0.111197</td>
      <td>Kern</td>
    </tr>
  </tbody>
</table>
</div>




```python
#collections.Counter(SanJQ_single.cdl_class_name)
```


```python
u'd'=='d'
```




    True




```python
cropN_mainCrop_dict = {u'Alfalfa':'Alfalfa',     
                  u'Almonds':'Al Pist',
                  u'Apples': 'Oth Dec',     
                  u'Apricots':'Oth Dec', 
                  u'Asparagus':'Oth Trk',   
                  u'Barley':'Grain', 
                  u'Broccoli':'Oth Trk', 
                  u'Cabbage':'Oth Trk',     
                  u'Camelina': 'Oth Fld',
                  u'Caneberries':'Oth Trk', 
                  u'Blueberries':'Oth Trk',
                  u'Canola':'Oth Fld',
                  u'Cantaloupes': 'Cucurb',
                  u'Carrots':'Oth Trk',     
                  u'Cauliflower':'Oth Trk', 
                  u'Cherries': 'Oth Dec',
                  u'Christmas Trees': 'Oth Trk',
                  u'Citrus':'Subtrop', 
                  u'Clover/Wildflowers':'Pasture',
                  u'Corn':'Corn', 
                  u'Cotton':'Cotton', 
                  u'Cranberries':'Oth Trk',
                  u'Cucumbers':'Cucurb', 
                  u'Dry Beans': 'DryBean',
                  u'Durum Wheat': 'Grain',
                  u'Garlic':'On Gar', 
                  u'Grapes':'Vine',
                  u'Grass/Pasture': "Pasture", 
                  u'Greens': "Oth Trk",
                  u'Herbs': 'Oth Trk',
                  u'Honeydew Melons': 'Cucurb', u'Lettuce': 'Oth Trk', 
                  u'Millet': 'Oth Fld',
                  u'Misc Vegs & Fruits': "Oth Dec",
                  u'Mustard': 'Oth Fld',                  
                  u'Nectarines': 'Oth Dec',
                  u'Oats': "Grain",
                  u'Olives': 'Subtrop', 
                  u'Onions': 'On Gar', 
                  u'Oranges': 'Subtrop',
                  u'Other Crops': 'Oth Fld',         
         u'Other Hay/Non Alfalfa': 'Grain',
         u'Other Tree Crops':'Oth Trk',
         u'Peaches': 'Oth Dec',
         u'Pears': 'Oth Dec',
         u'Peas': 'Oth Trk',
         u'Pecans': 'Oth Dec',
         u'Peppers': 'Oth Trk',
         u'Pistachios': 'Al Pist',
         u'Plums': 'Oth Dec',
         u'Pomegranates': 'Oth Dec',           
         u'Pop or Orn Corn': 'Corn',
         u'Potatoes': 'Potato',
         u'Prunes': 'Oth Dec',
         u'Pumpkins': 'Cucurb',
         u'Radishes': "SgrBeet",        
         u'Rice': 'Rice',
         u'Rye': 'Grain',
         u'Safflower': 'Safflwr',
         u'Sod/Grass Seed': 'Pasture',
         u'Sorghum': 'Oth Fld',
         u'Soybeans': 'DryBean',
         u'Spring Wheat': 'Grain',
         u'Squash': 'Cucurb',
         u'Strawberries': 'Oth Trk',
         u'Sugarbeets': 'SgrBeet',
         u'Sunflower': 'Oth Fld',
         u'Sweet Corn': 'Corn',
         u'Sweet Potatoes': 'Potato',
         u'Tomatoes': 'Pr Tom',
         u'Triticale': 'Grain',
         u'Turnips': 'SgrBeet',                           
         u'Vetch': 'Oth Trk',
         u'Walnuts': 'Oth Dec',
         u'Watermelons': 'Cucurb',
         u'Winter Wheat': 'Grain'}
```


```python
my_map = cropN_mainCrop_dict.copy()
inv_map = {}
for k, v in my_map.iteritems():
    inv_map[v] = inv_map.get(v, [])
    inv_map[v].append(k)
print inv_map.keys()    
inv_map
```

    ['Alfalfa', 'Cucurb', 'Potato', 'Vine', 'Corn', 'On Gar', 'Oth Dec', 'DryBean', 'Cotton', 'Oth Trk', 'Oth Fld', 'Grain', 'Al Pist', 'Safflwr', 'Pasture', 'Subtrop', 'Rice', 'Pr Tom', 'SgrBeet']





    {'Al Pist': [u'Almonds', u'Pistachios'],
     'Alfalfa': [u'Alfalfa'],
     'Corn': [u'Corn', u'Sweet Corn', u'Pop or Orn Corn'],
     'Cotton': [u'Cotton'],
     'Cucurb': [u'Cantaloupes',
      u'Pumpkins',
      u'Honeydew Melons',
      u'Squash',
      u'Watermelons',
      u'Cucumbers'],
     'DryBean': [u'Dry Beans', u'Soybeans'],
     'Grain': [u'Barley',
      u'Spring Wheat',
      u'Durum Wheat',
      u'Triticale',
      u'Other Hay/Non Alfalfa',
      u'Rye',
      u'Winter Wheat',
      u'Oats'],
     'On Gar': [u'Garlic', u'Onions'],
     'Oth Dec': [u'Pears',
      u'Apricots',
      u'Misc Vegs & Fruits',
      u'Pomegranates',
      u'Cherries',
      u'Nectarines',
      u'Plums',
      u'Walnuts',
      u'Prunes',
      u'Apples',
      u'Pecans',
      u'Peaches'],
     'Oth Fld': [u'Sunflower',
      u'Other Crops',
      u'Sorghum',
      u'Camelina',
      u'Canola',
      u'Mustard',
      u'Millet'],
     'Oth Trk': [u'Blueberries',
      u'Vetch',
      u'Peppers',
      u'Other Tree Crops',
      u'Peas',
      u'Broccoli',
      u'Asparagus',
      u'Carrots',
      u'Cranberries',
      u'Cauliflower',
      u'Lettuce',
      u'Herbs',
      u'Strawberries',
      u'Cabbage',
      u'Greens',
      u'Christmas Trees',
      u'Caneberries'],
     'Pasture': [u'Clover/Wildflowers', u'Grass/Pasture', u'Sod/Grass Seed'],
     'Potato': [u'Sweet Potatoes', u'Potatoes'],
     'Pr Tom': [u'Tomatoes'],
     'Rice': [u'Rice'],
     'Safflwr': [u'Safflower'],
     'SgrBeet': [u'Radishes', u'Sugarbeets', u'Turnips'],
     'Subtrop': [u'Oranges', u'Olives', u'Citrus'],
     'Vine': [u'Grapes']}




```python
SanJQ_single["Crop_Name"] = SanJQ_single["cdl_class_name"].map(cropN_mainCrop_dict)
```


```python
##
cdl_null_df = SanJQ_single[pd.isnull(SanJQ_single).any(axis=1)]
print SanJQ_single.shape
print cdl_null_df.shape
collections.Counter(cdl_null_df.cdl_class_name)
```

    (7055, 7)
    (1357, 7)





    Counter({u'Aquaculture': 5,
             u'Barren': 108,
             u'Deciduous Forest': 86,
             u'Developed/High Intensity': 108,
             u'Developed/Low Intensity': 108,
             u'Developed/Med Intensity': 108,
             u'Developed/Open Space': 108,
             u'Evergreen Forest': 89,
             u'Fallow/Idle Cropland': 108,
             u'Forest': 8,
             u'Herbaceous Wetlands': 106,
             u'Mixed Forest': 91,
             u'Open Water': 108,
             u'Shrubland': 108,
             u'Wetlands': 6,
             u'Woody Wetlands': 102})




```python
print 7055 - 1357
SanJQ_single = SanJQ_single.dropna()
SanJQ_single.shape
```

    5698





    (5698, 7)




```python
SanJQ_single.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>county</th>
      <th>Crop_Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
      <td>San Joaquin</td>
      <td>Oth Dec</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
      <td>San Joaquin</td>
      <td>Vine</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
      <td>San Joaquin</td>
      <td>Corn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
      <td>San Joaquin</td>
      <td>Al Pist</td>
    </tr>
  </tbody>
</table>
</div>




```python
pwd
```




    u'/Users/yanlinli/Dropbox/141groupprj/OriginalData'




```python
path='/Users/yanlinli/Dropbox/141groupprj/OriginalData'
os.listdir(path)

```




    ['.DS_Store',
     'Ag_2010.xlsx',
     'cdl_ca_gw_basins.xlsx',
     'Lati_Longi.xlsx',
     'OriginalData copy',
     'OtherTxt',
     'precipitation.xlsx',
     'Sq_long_La_16Sub.xlsx',
     'SubB_Yr_Cnty_Crp_Wtr_Acr_Zip_Prcip.xlsx',
     'WaterUsage_Per_Crop_2010.xlsx']




```python
Ag_2010 = pd.read_excel('Ag_2010.xlsx')
```


```python
Ag_2010 = Ag_2010.drop('Year', 1)
Ag_2010.index = Ag_2010['Co_Name']
Ag_2010.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Co_Name</th>
      <th>Grain AW WA</th>
      <th>Rice AW WA</th>
      <th>Cotton AW WA</th>
      <th>SgrBeet AW WA</th>
      <th>Corn AW WA</th>
      <th>DryBean AW WA</th>
      <th>Safflwr AW WA</th>
      <th>Oth Fld AW WA</th>
      <th>Alfalfa AW WA</th>
      <th>...</th>
      <th>Pr Tom AW WA</th>
      <th>Fr Tom AW WA</th>
      <th>Cucurb AW WA</th>
      <th>On Gar AW WA</th>
      <th>Potato AW WA</th>
      <th>Oth Trk AW WA</th>
      <th>Al Pist AW WA</th>
      <th>Oth Dec AW WA</th>
      <th>Subtrop AW WA</th>
      <th>Vine AW WA</th>
    </tr>
    <tr>
      <th>Co_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alameda</th>
      <td>Alameda</td>
      <td>1.227136</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>5.566410</td>
      <td>...</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>3.322419</td>
      <td>4.012059</td>
      <td>4.089118</td>
      <td>3.200228</td>
      <td>1.322920</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>Alpine</td>
      <td>1.036609</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>3.979483</td>
      <td>...</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.745486</td>
      <td>3.435330</td>
      <td>3.093030</td>
      <td>2.750411</td>
      <td>1.473550</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>Amador</td>
      <td>0.152481</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.703687</td>
      <td>3.511449</td>
      <td>...</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>2.418772</td>
      <td>3.435330</td>
      <td>2.729704</td>
      <td>2.750411</td>
      <td>0.581198</td>
    </tr>
    <tr>
      <th>Butte</th>
      <td>Butte</td>
      <td>0.151040</td>
      <td>4.200113</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.508677</td>
      <td>0.876382</td>
      <td>1.660225</td>
      <td>3.151581</td>
      <td>...</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>0.983734</td>
      <td>2.164283</td>
      <td>2.720195</td>
      <td>1.758203</td>
      <td>2.264204</td>
      <td>2.192851</td>
      <td>1.919587</td>
      <td>1.585771</td>
    </tr>
    <tr>
      <th>Calaveras</th>
      <td>Calaveras</td>
      <td>0.258701</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>1.517600</td>
      <td>3.519420</td>
      <td>...</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.063208</td>
      <td>3.435330</td>
      <td>2.741638</td>
      <td>2.401690</td>
      <td>0.664280</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
Ag_2010 = Ag_2010.drop('Co_Name', 1)
Ag_2010.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grain AW WA</th>
      <th>Rice AW WA</th>
      <th>Cotton AW WA</th>
      <th>SgrBeet AW WA</th>
      <th>Corn AW WA</th>
      <th>DryBean AW WA</th>
      <th>Safflwr AW WA</th>
      <th>Oth Fld AW WA</th>
      <th>Alfalfa AW WA</th>
      <th>Pasture AW WA</th>
      <th>Pr Tom AW WA</th>
      <th>Fr Tom AW WA</th>
      <th>Cucurb AW WA</th>
      <th>On Gar AW WA</th>
      <th>Potato AW WA</th>
      <th>Oth Trk AW WA</th>
      <th>Al Pist AW WA</th>
      <th>Oth Dec AW WA</th>
      <th>Subtrop AW WA</th>
      <th>Vine AW WA</th>
    </tr>
    <tr>
      <th>Co_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alameda</th>
      <td>1.227136</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>5.566410</td>
      <td>4.150807</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>3.322419</td>
      <td>4.012059</td>
      <td>4.089118</td>
      <td>3.200228</td>
      <td>1.322920</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>1.036609</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>3.979483</td>
      <td>4.191053</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.745486</td>
      <td>3.435330</td>
      <td>3.093030</td>
      <td>2.750411</td>
      <td>1.473550</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>0.152481</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.703687</td>
      <td>3.511449</td>
      <td>3.753556</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>2.418772</td>
      <td>3.435330</td>
      <td>2.729704</td>
      <td>2.750411</td>
      <td>0.581198</td>
    </tr>
    <tr>
      <th>Butte</th>
      <td>0.151040</td>
      <td>4.200113</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.508677</td>
      <td>0.876382</td>
      <td>1.660225</td>
      <td>3.151581</td>
      <td>3.446727</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>0.983734</td>
      <td>2.164283</td>
      <td>2.720195</td>
      <td>1.758203</td>
      <td>2.264204</td>
      <td>2.192851</td>
      <td>1.919587</td>
      <td>1.585771</td>
    </tr>
    <tr>
      <th>Calaveras</th>
      <td>0.258701</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>1.517600</td>
      <td>3.519420</td>
      <td>3.477850</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.063208</td>
      <td>3.435330</td>
      <td>2.741638</td>
      <td>2.401690</td>
      <td>0.664280</td>
    </tr>
  </tbody>
</table>
</div>




```python
Ag_2010.rename(columns=lambda x: x.replace('AW', '').replace('WA','').strip(), inplace=True)
```


```python
Ag_2010.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grain</th>
      <th>Rice</th>
      <th>Cotton</th>
      <th>SgrBeet</th>
      <th>Corn</th>
      <th>DryBean</th>
      <th>Safflwr</th>
      <th>Oth Fld</th>
      <th>Alfalfa</th>
      <th>Pasture</th>
      <th>Pr Tom</th>
      <th>Fr Tom</th>
      <th>Cucurb</th>
      <th>On Gar</th>
      <th>Potato</th>
      <th>Oth Trk</th>
      <th>Al Pist</th>
      <th>Oth Dec</th>
      <th>Subtrop</th>
      <th>Vine</th>
    </tr>
    <tr>
      <th>Co_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alameda</th>
      <td>1.227136</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>5.566410</td>
      <td>4.150807</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>3.322419</td>
      <td>4.012059</td>
      <td>4.089118</td>
      <td>3.200228</td>
      <td>1.322920</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>1.036609</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.226513</td>
      <td>3.979483</td>
      <td>4.191053</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.745486</td>
      <td>3.435330</td>
      <td>3.093030</td>
      <td>2.750411</td>
      <td>1.473550</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>0.152481</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>2.703687</td>
      <td>3.511449</td>
      <td>3.753556</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>2.418772</td>
      <td>3.435330</td>
      <td>2.729704</td>
      <td>2.750411</td>
      <td>0.581198</td>
    </tr>
    <tr>
      <th>Butte</th>
      <td>0.151040</td>
      <td>4.200113</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.508677</td>
      <td>0.876382</td>
      <td>1.660225</td>
      <td>3.151581</td>
      <td>3.446727</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>0.983734</td>
      <td>2.164283</td>
      <td>2.720195</td>
      <td>1.758203</td>
      <td>2.264204</td>
      <td>2.192851</td>
      <td>1.919587</td>
      <td>1.585771</td>
    </tr>
    <tr>
      <th>Calaveras</th>
      <td>0.258701</td>
      <td>4.885808</td>
      <td>3.5756</td>
      <td>3.209961</td>
      <td>2.263332</td>
      <td>1.940346</td>
      <td>1.601214</td>
      <td>1.517600</td>
      <td>3.519420</td>
      <td>3.477850</td>
      <td>2.427646</td>
      <td>1.978039</td>
      <td>1.332642</td>
      <td>2.638490</td>
      <td>2.720195</td>
      <td>1.063208</td>
      <td>3.435330</td>
      <td>2.741638</td>
      <td>2.401690</td>
      <td>0.664280</td>
    </tr>
  </tbody>
</table>
</div>




```python
#but i don't know how to creat 2d df from here 
unstack_df = pd.DataFrame(Ag_2010.unstack())
unstack_df.head()
#unstack_df.index.levels
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>0</th>
    </tr>
    <tr>
      <th></th>
      <th>Co_Name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Grain</th>
      <th>Alameda</th>
      <td>1.227136</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>1.036609</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>0.152481</td>
    </tr>
    <tr>
      <th>Butte</th>
      <td>0.151040</td>
    </tr>
    <tr>
      <th>Calaveras</th>
      <td>0.258701</td>
    </tr>
  </tbody>
</table>
</div>




```python
from itertools import chain
county_list = []
for i in Ag_2010.index:
    county_list.append([i]*20) 
county_list = list(chain(*county_list))
print 'county list len', len(county_list)  
crop_list = list(chain(*([Ag_2010.columns.values]*57)))
len(crop_list )
```

    county list len 1140





    1140




```python
Ag_2010_df = pd.DataFrame(list(chain(*Ag_2010.values)))
Ag_2010_df = Ag_2010_df.rename(columns={0:'WaterUsagePerAcre'})
Ag_2010_df['County'] =  pd.DataFrame(county_list)
Ag_2010_df['Crop'] =  pd.DataFrame(crop_list)
Ag_2010_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>WaterUsagePerAcre</th>
      <th>County</th>
      <th>Crop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.227136</td>
      <td>Alameda</td>
      <td>Grain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.885808</td>
      <td>Alameda</td>
      <td>Rice</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.575600</td>
      <td>Alameda</td>
      <td>Cotton</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.209961</td>
      <td>Alameda</td>
      <td>SgrBeet</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.263332</td>
      <td>Alameda</td>
      <td>Corn</td>
    </tr>
  </tbody>
</table>
</div>




```python
print set(collections.Counter(SanJQ_single.Crop_Name))
print len(set(collections.Counter(SanJQ_single.Crop_Name)))
print set(collections.Counter(Ag_2010_df.Crop))
print len(set(collections.Counter(Ag_2010_df.Crop)))
print set(collections.Counter(Ag_2010_df.Crop))& set(collections.Counter(SanJQ_single.Crop_Name))
print len(set(collections.Counter(Ag_2010_df.Crop))&set(collections.Counter(SanJQ_single.Crop_Name)))
```

    set(['Alfalfa', 'Cucurb', 'Potato', 'Oth Dec', 'Corn', 'On Gar', 'Vine', 'DryBean', 'Cotton', 'Oth Trk', 'Oth Fld', 'Grain', 'Al Pist', 'Safflwr', 'Pasture', 'Subtrop', 'Rice', 'Pr Tom', 'SgrBeet'])
    19
    set([u'Alfalfa', u'Cucurb', u'SgrBeet', u'Potato', u'Oth Dec', u'Corn', u'On Gar', u'Vine', u'Oth Fld', u'DryBean', u'Oth Trk', u'Fr Tom', u'Grain', u'Al Pist', u'Safflwr', u'Pasture', u'Subtrop', u'Rice', u'Pr Tom', u'Cotton'])
    20
    set(['Alfalfa', 'Cucurb', 'SgrBeet', 'Potato', 'Vine', 'Corn', 'On Gar', 'Oth Dec', 'DryBean', 'Oth Trk', 'Oth Fld', 'Grain', 'Al Pist', 'Safflwr', 'Pasture', 'Subtrop', 'Rice', 'Pr Tom', 'Cotton'])
    19



```python
print set(collections.Counter(SanJQ_single.county))
set(collections.Counter(Ag_2010_df.County))& set(collections.Counter(SanJQ_single.county))
```

    set(['San Joaquin', 'Fresno', 'Merced', 'Kern', 'Madera', 'Kings', 'Tulare', 'Stanislaus'])





    {'Fresno',
     'Kern',
     'Kings',
     'Madera',
     'Merced',
     'San Joaquin',
     'Stanislaus',
     'Tulare'}




```python
SanJQ_single = SanJQ_single.rename(columns={'county':'County','Crop_Name':'Crop'})
print SanJQ_single.shape
print SanJQ_single.shape
SanJQ_single.head()
```

    (5698, 7)
    (5698, 7)





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>County</th>
      <th>Crop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Walnuts</td>
      <td>73249.299965</td>
      <td>San Joaquin</td>
      <td>Oth Dec</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grapes</td>
      <td>62451.585532</td>
      <td>San Joaquin</td>
      <td>Vine</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Corn</td>
      <td>55180.608525</td>
      <td>San Joaquin</td>
      <td>Corn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>48995.140747</td>
      <td>San Joaquin</td>
      <td>Al Pist</td>
    </tr>
  </tbody>
</table>
</div>




```python
ALL = pd.merge(SanJQ_single, Ag_2010_df, on=['County', 'Crop'])
ALL.shape
ALL = ALL.drop('Basin_Name',1)
```


```python
print sum(ALL.isnull().any(axis=1))
ALL.head()
```

    0





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Grass/Pasture</td>
      <td>238527.587650</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
      <td>5.139264</td>
    </tr>
    <tr>
      <th>1</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Clover/Wildflowers</td>
      <td>4893.576132</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
      <td>5.139264</td>
    </tr>
    <tr>
      <th>2</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2010</td>
      <td>Sod/Grass Seed</td>
      <td>2493.490983</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
      <td>5.139264</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Grass/Pasture</td>
      <td>238056.332977</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
      <td>5.139264</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>2011</td>
      <td>Clover/Wildflowers</td>
      <td>5796.054407</td>
      <td>San Joaquin</td>
      <td>Pasture</td>
      <td>5.139264</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(ALL.Subbasin_N)
print collections.Counter(ALL.County)
list(ALL)
```

    Counter({'Stanislaus': 1070, 'San Joaquin': 1027, 'Kings': 892, 'Tulare': 684, 'Madera': 622, 'Kern': 572, 'Fresno': 492, 'Merced': 339})





    [u'Subbasin_N',
     u'year',
     u'cdl_class_name',
     u'acres',
     'County',
     'Crop',
     'WaterUsagePerAcre']




```python
ALL[(ALL.Subbasin_N =='CHOWCHILLA') & (ALL.year ==2010) & (ALL.County=='Madera') & (ALL.Crop =='Al Pist')]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>cdl_class_name</th>
      <th>acres</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2448</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Almonds</td>
      <td>32844.160041</td>
      <td>Madera</td>
      <td>Al Pist</td>
      <td>3.344023</td>
    </tr>
    <tr>
      <th>2449</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Pistachios</td>
      <td>4114.304601</td>
      <td>Madera</td>
      <td>Al Pist</td>
      <td>3.344023</td>
    </tr>
  </tbody>
</table>
</div>




```python
32844.160041+4114.304601 #match the fisrt number in the below df 
```




    36958.464642000006




```python
f = {'acres':['sum'] }
ALL_merge = ALL.groupby([u'Subbasin_N', u'year',
             u'County', u'Crop', u'WaterUsagePerAcre']).agg(f)
```


```python
ALL_merge.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th>acres</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th>sum</th>
    </tr>
    <tr>
      <th>Subbasin_N</th>
      <th>year</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">CHOWCHILLA</th>
      <th rowspan="5" valign="top">2010</th>
      <th rowspan="5" valign="top">Madera</th>
      <th>Al Pist</th>
      <th>3.344023</th>
      <td>36958.464642</td>
    </tr>
    <tr>
      <th>Alfalfa</th>
      <th>4.318180</th>
      <td>34392.028150</td>
    </tr>
    <tr>
      <th>Corn</th>
      <th>2.545571</th>
      <td>6004.104783</td>
    </tr>
    <tr>
      <th>Cotton</th>
      <th>3.152639</th>
      <td>3535.633219</td>
    </tr>
    <tr>
      <th>Cucurb</th>
      <th>1.605352</th>
      <td>163.237815</td>
    </tr>
  </tbody>
</table>
</div>




```python
print ALL_merge.shape
ALL.shape
```

    (1879, 1)





    (5698, 7)




```python
Names = pd.DataFrame([ALL_merge.ix[i,].name for i in range(0,1879)])
Values = pd.DataFrame([ALL_merge.ix[i,].values for i in range(0,1879)])
ALL2 = pd.concat([Names, Values], axis=1,ignore_index=True)
```


```python
ALL2.shape
```




    (1879, 6)




```python
Values.shape
```




    (1879, 1)




```python
ALL2 = ALL2.rename(columns = {0:u'Subbasin_N', 1:u'Year', 2:'County',
                       3:u'Crop',4:u'WaterUsagePerAcre', 5:u'Acre'})
print ALL2.shape
ALL2.head()
```

    (1879, 6)





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>Year</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
      <th>Acre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Al Pist</td>
      <td>3.344023</td>
      <td>36958.464642</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Alfalfa</td>
      <td>4.318180</td>
      <td>34392.028150</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Corn</td>
      <td>2.545571</td>
      <td>6004.104783</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cotton</td>
      <td>3.152639</td>
      <td>3535.633219</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cucurb</td>
      <td>1.605352</td>
      <td>163.237815</td>
    </tr>
  </tbody>
</table>
</div>




```python
path='/Users/yanlinli/Dropbox/141groupprj/OriginalData'
os.listdir(path)

```




    ['.DS_Store',
     'Ag_2010.xlsx',
     'cdl_ca_gw_basins.xlsx',
     'Lati_Longi.xlsx',
     'OriginalData copy',
     'OtherTxt',
     'precipitation.xlsx',
     'Sq_long_La_16Sub.xlsx',
     'SubB_Yr_Cnty_Crp_Wtr_Acr_Zip_Prcip.xlsx',
     'SubB_Yr_Cnty_Crp_Wtr_Acr_Zip_Prcip_Ecn.xlsx',
     'WaterUsage_Per_Crop_2010.xlsx']




```python
precipitation = pd.read_excel('precipitation.xlsx')
```


```python
collections.Counter(ALL2.County)
```




    Counter({'Fresno': 191,
             'Kern': 196,
             'Kings': 300,
             'Madera': 213,
             'Merced': 110,
             'San Joaquin': 324,
             'Stanislaus': 330,
             'Tulare': 215})




```python
collections.Counter(precipitation.County_N)
```




    Counter({u'Fresno': 6,
             u'Kern': 6,
             u'Kings': 6,
             u'Madera': 6,
             u'Merced': 6,
             u'San Joaquin': 6,
             u'Stanislaus': 6,
             u'Tulare': 6})




```python
precipitation = precipitation.rename(columns = {'County_N':u'County','year':u'Year'})
```


```python
precipitation.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>County</th>
      <th>zipcode</th>
      <th>Year</th>
      <th>Precip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fresno</td>
      <td>93210</td>
      <td>2010</td>
      <td>7.273551</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Fresno</td>
      <td>93210</td>
      <td>2011</td>
      <td>6.897796</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fresno</td>
      <td>93210</td>
      <td>2012</td>
      <td>1.789807</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fresno</td>
      <td>93210</td>
      <td>2013</td>
      <td>2.816295</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fresno</td>
      <td>93210</td>
      <td>2014</td>
      <td>5.495055</td>
    </tr>
  </tbody>
</table>
</div>




```python
ALL3 = pd.merge(ALL2, precipitation, on=['County', 'Year'])
```


```python
ALL3.shape
```




    (1879, 8)




```python
ALL3.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>Year</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
      <th>Acre</th>
      <th>zipcode</th>
      <th>Precip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Al Pist</td>
      <td>3.344023</td>
      <td>36958.464642</td>
      <td>93638</td>
      <td>14.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Alfalfa</td>
      <td>4.318180</td>
      <td>34392.028150</td>
      <td>93638</td>
      <td>14.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Corn</td>
      <td>2.545571</td>
      <td>6004.104783</td>
      <td>93638</td>
      <td>14.15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cotton</td>
      <td>3.152639</td>
      <td>3535.633219</td>
      <td>93638</td>
      <td>14.15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cucurb</td>
      <td>1.605352</td>
      <td>163.237815</td>
      <td>93638</td>
      <td>14.15</td>
    </tr>
  </tbody>
</table>
</div>




```python
#ALL3.to_excel('SubB_Yr_Cnty_Crp_Wtr_Acr_Zip_Prcip.xlsx', sheet_name='sheet1', index=False)
```


```python
pwd
```




    u'/Users/yanlinli/Dropbox/141groupprj/OriginalData'




```python
#cropN_mainCrop_dict
```


```python
CropGroup = pd.DataFrame(cropN_mainCrop_dict.items())
CropGroup = CropGroup.rename(columns = {0:u'SubCrop',1:u'Crop'})
CropGroup.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SubCrop</th>
      <th>Crop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cantaloupes</td>
      <td>Cucurb</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Olives</td>
      <td>Subtrop</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Blueberries</td>
      <td>Oth Trk</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Durum Wheat</td>
      <td>Grain</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rye</td>
      <td>Grain</td>
    </tr>
  </tbody>
</table>
</div>




```python
collections.Counter(ALL3.Subbasin_N)
##u'KETTLEMAN PLAIN': 84,
##u'WHITE WOLF': 88})                 
#Sq.to_excel('Sq_long_La_16Sub.xlsx', sheet_name='sheet1', index=False)
```




    Counter({u'CHOWCHILLA': 106,
             u'COSUMNES': 104,
             u'DELTA-MENDOTA': 112,
             u'EASTERN SAN JOAQUIN': 110,
             u'KAWEAH': 109,
             u'KERN COUNTY': 108,
             u'KETTLEMAN PLAIN': 84,
             u'KINGS': 111,
             u'MADERA': 107,
             u'MERCED': 110,
             u'MODESTO': 110,
             u'PLEASANT VALLEY': 82,
             u'TRACY': 110,
             u'TULARE LAKE': 105,
             u'TULE': 106,
             u'TURLOCK': 108,
             u'WESTSIDE': 109,
             u'WHITE WOLF': 88})




```python
collections.Counter(ALL3.County)
```




    Counter({'Fresno': 191,
             'Kern': 196,
             'Kings': 300,
             'Madera': 213,
             'Merced': 110,
             'San Joaquin': 324,
             'Stanislaus': 330,
             'Tulare': 215})




```python
SqLL = pd.read_excel('Sq_long_La_16Sub.xlsx')
```


```python
#SqLL.head()
#collections.Counter(SqLL.Subbasin_N)
```


```python
collections.Counter(ALL3.Crop).keys()
```




    ['Alfalfa',
     'Cucurb',
     'SgrBeet',
     'Potato',
     'Vine',
     'Corn',
     'On Gar',
     'Oth Dec',
     'DryBean',
     'Oth Trk',
     'Oth Fld',
     'Grain',
     'Al Pist',
     'Safflwr',
     'Pasture',
     'Subtrop',
     'Rice',
     'Pr Tom',
     'Cotton']




```python
# data from price value in 2013 
# econ value is dollar per acers
def avg(l):
    return sum(l, 0.0) / len(l)

Econ_dict = { "Al Pist":2360*3.21, 
         "Alfalfa":7.0*206.00,
         "Corn": 26.50*48.23,
         "Cotton":1628*140.00, 
         "Cucurb":avg([260*20.20, 180*35.40, 200*25.90,580*13.00,300*16.00,330*15.60]),
#Honeydew Melons  260 2,730,000 20.20 Cwt. Cwt. $/Cwt.
#"Squash"   180 1,224,000 35.40   Cwt. Cwt. $/Cwt.
#"Cucumbers"  200 760,000 25.90   Cwt. Cwt. $/Cwt.
#"Watermelons"  580 5,800,000 13.00  Cwt. Cwt. $/Cwt.
#"Cantaloupes"   300 12,750,000 16.00  Cwt. Cwt. $/Cwt.
#"Pumpkins    330 1,947,000 15.60   Cwt. Cwt. $/Cwt.

         "DryBean": 2320*56.80, 
         "Grain":5.35*190.36,
         "On Gar":avg([ 400*13.20,165*60.30 ]), 
#"Onions"  spring 400 2,720,000 13.20   summer  490 3,822,000 6.40   Onions, Summer Storage 399 11,700,000 9.11
# "Garlic"   165 3,795,000 60.30
         "Oth Dec":avg([ 8.88*466  ,5.73*682  ,2.48*3390  ,19.00*391,8.33*780,14.10*429 ,5.30*664 , 1.76 *3710,1750*2.06    ]),
#"Apples" 8.88 135,000 466  Tons Tons $/Ton
#"Apricots"  5.73 54,400 682   Tons Tons $/Ton
#"Cherries", 2.48 82,000 3,390  Tons Tons $/Ton
#"Pears",  19.00 220,000 391  Tons Tons $/Ton
#"Nectarines"  8.33 150,000 780 Tons Tons $/Ton
#"Peaches", 14.10 648,000 429 Tons Tons $/Ton
#"Plums",  5.30 95,400 664   Tons Tons $/Ton
#"Walnuts" 1.76 492,000 3,710  #tones Tons $/Ton
#"Pecans"  1,750  5,000 2.06  Pounds 1000pounds $/Pound
         "Oth Fld":avg([1296.00* 27.1, 17.00*37.56]),
# sunflowers 1,296.00 751,500 27.1   Tons Tons $/Ton
 # Sorghum2009   17.00 646,000 37.56   Tons Tons $/Ton
         "Oth Trk":avg([320*29.60, 350*24.90, 32*152.00, 180*42.70, 107*248.00,425*41.70,385* 38.70 ,165*42.10,405*21.70 ]),
#"Carrots" 320 20,000,000 29.60  Cwt. Cwt. $/Cwt.
#"Lettuce"  350 33,600,000 24.90 Cwt. Cwt. $/Cwt.
#"Asparagus"  32  368,000  152.00  Cwt. Cwt. $/Cwt.
#"Cauliflower"  180 5,868,000 42.70  Cwt. Cwt. $/Cwt.
# berries  107 514,000 248.00 Cwt. Cwt. $/Cwt.
# "Peppers Bell", 425 8,465,000 41.70  Cwt. Cwt. $/Cwt.
# pepers Chile    385 2,640,000 38.70   Cwt. Cwt. $/Cwt.
# "Broccoli",  165 20,460,000 42.10 8   Cwt. Cwt. $/Cwt.
# "Cabbage",  405 5,670,000 21.70   Cwt. Cwt. $/Cwt.
         "Pasture":0, 
         "Potato":425*17.1, # Cwt. Cwt. $/Cwt.
         "Pro Tom":300*36.20, # Cwt. Cwt. $/Cwt 
         "Rice":84.80*20.9, # Cwt. Cwt. $/Cwt
         "Safflwr": 2000.00*26.5, #  Pounds Cwt. $/Cwt.
         "SgrBeet": 43.40*52.1,  # Tons Tons $/Ton
          "Subtrop":avg([622*6.52,4.15*813  ]), 
# orange 622 109000000 6.52
# Olives  4.15 166000 813  Tons Tons $/Ton
          "Vine":900*5.07}# Cartons 3/ Cartons $/Carton


Econ_dict
```




    {'Al Pist': 7575.6,
     'Alfalfa': 1442.0,
     'Corn': 1278.095,
     'Cotton': 227920.0,
     'Cucurb': 5715.333333333333,
     'DryBean': 131776.0,
     'Grain': 1018.426,
     'On Gar': 7614.75,
     'Oth Dec': 5564.693333333333,
     'Oth Fld': 17880.059999999998,
     'Oth Trk': 11736.666666666666,
     'Pasture': 0,
     'Potato': 7267.500000000001,
     'Pro Tom': 10860.0,
     'Rice': 1772.3199999999997,
     'Safflwr': 53000.0,
     'SgrBeet': 2261.14,
     'Subtrop': 3714.6949999999997,
     'Vine': 4563.0}




```python
ALL3["EcnValue"] = ALL3["Crop"].map(Econ_dict)
ALL3.to_excel('SubB_Yr_Cnty_Crp_Wtr_Acr_Zip_Prcip_Ecn.xlsx', sheet_name='sheet1', index=False)
```


```python
ALL3.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>Year</th>
      <th>County</th>
      <th>Crop</th>
      <th>WaterUsagePerAcre</th>
      <th>Acre</th>
      <th>zipcode</th>
      <th>Precip</th>
      <th>EcnValue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Al Pist</td>
      <td>3.344023</td>
      <td>36958.464642</td>
      <td>93638</td>
      <td>14.15</td>
      <td>7575.600000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Alfalfa</td>
      <td>4.318180</td>
      <td>34392.028150</td>
      <td>93638</td>
      <td>14.15</td>
      <td>1442.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Corn</td>
      <td>2.545571</td>
      <td>6004.104783</td>
      <td>93638</td>
      <td>14.15</td>
      <td>1278.095000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cotton</td>
      <td>3.152639</td>
      <td>3535.633219</td>
      <td>93638</td>
      <td>14.15</td>
      <td>227920.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHOWCHILLA</td>
      <td>2010</td>
      <td>Madera</td>
      <td>Cucurb</td>
      <td>1.605352</td>
      <td>163.237815</td>
      <td>93638</td>
      <td>14.15</td>
      <td>5715.333333</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```


```python
SqLL = pd.read_excel('Sq_long_La_16Sub.xlsx')
print SqLL.shape
SqLL.head()

```

    (18675, 4)





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Basin_Name</th>
      <th>Subbasin_N</th>
      <th>longitude</th>
      <th>latitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>-119.088229</td>
      <td>35.791916</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>-119.088728</td>
      <td>35.790731</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>-119.012405</td>
      <td>35.790597</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>-119.009633</td>
      <td>35.790596</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SAN JOAQUIN VALLEY</td>
      <td>KERN COUNTY</td>
      <td>-119.009541</td>
      <td>35.790596</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(SqLL)
print SqLL.latitude.dtype
print SqLL.longitude.dtype
Sub_Lon_Lat = SqLL.groupby(['Subbasin_N']).mean()
Sub_Lon_Lat = Sub_Lon_Lat.reset_index(True)
```

    float64
    float64



```python
Sub_Lon_Lat
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subbasin_N</th>
      <th>longitude</th>
      <th>latitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CHOWCHILLA</td>
      <td>-120.341671</td>
      <td>37.090853</td>
    </tr>
    <tr>
      <th>1</th>
      <td>COSUMNES</td>
      <td>-121.078087</td>
      <td>38.330043</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DELTA-MENDOTA</td>
      <td>-120.929047</td>
      <td>37.041357</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EASTERN SAN JOAQUIN</td>
      <td>-121.036118</td>
      <td>38.016319</td>
    </tr>
    <tr>
      <th>4</th>
      <td>KAWEAH</td>
      <td>-119.080095</td>
      <td>36.307722</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KERN COUNTY</td>
      <td>-119.319665</td>
      <td>35.317558</td>
    </tr>
    <tr>
      <th>6</th>
      <td>KETTLEMAN PLAIN</td>
      <td>-120.011155</td>
      <td>35.872416</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KINGS</td>
      <td>-119.504783</td>
      <td>36.685465</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MADERA</td>
      <td>-119.917505</td>
      <td>37.030662</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MERCED</td>
      <td>-120.427700</td>
      <td>37.328021</td>
    </tr>
    <tr>
      <th>10</th>
      <td>MODESTO</td>
      <td>-120.770918</td>
      <td>37.715208</td>
    </tr>
    <tr>
      <th>11</th>
      <td>PLEASANT VALLEY</td>
      <td>-120.110955</td>
      <td>35.964013</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TRACY</td>
      <td>-121.603805</td>
      <td>37.873860</td>
    </tr>
    <tr>
      <th>13</th>
      <td>TULARE LAKE</td>
      <td>-119.722563</td>
      <td>36.229246</td>
    </tr>
    <tr>
      <th>14</th>
      <td>TULE</td>
      <td>-119.005959</td>
      <td>35.987088</td>
    </tr>
    <tr>
      <th>15</th>
      <td>TURLOCK</td>
      <td>-120.742345</td>
      <td>37.520860</td>
    </tr>
    <tr>
      <th>16</th>
      <td>WESTSIDE</td>
      <td>-120.404486</td>
      <td>36.440500</td>
    </tr>
    <tr>
      <th>17</th>
      <td>WHITE WOLF</td>
      <td>-118.876929</td>
      <td>35.032244</td>
    </tr>
  </tbody>
</table>
</div>




```python
Sub_Lon_Lat.to_excel('18Sub_Lon_Lat.xlsx', sheet_name='sheet1', index=False)
```
