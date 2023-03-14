# Prediksi Harga Rumah Berdasarkan Kemiripan Atribut
Script ini berisi code yang mengembalikan nilai 'harga' berdasarkan suatu data dengan format data = {'tanah': x, 'bangunan': y, 'jarak_ke_pusat':z} dimana x,y,z adalah int/float dan 'tanah' adalah luas tanah, 'bangunan' adalah luas bangunan, dan 'jarak_ke_pusat' adalah jarak dari lokasi ke pusat kota.

## Dataset yang digunakan:
Harga Rumah di Tangerang: click [here](https://storage.googleapis.com/dqlab-dataset/harga_rumah.txt)

## Functions Explanation:
- get_all_specified_attributes()
- min_value(), max_value()
- transform_attribute()
- data_transformation()
- transform_data()
- price_based_on_similarity()

### 1. get_all_specified_attribute (list_of_dictionary,specified_key):
Mengembalikan nilai seluruh value dari suatu key. Code
```code
    get_all_specified_attribute(harga_rumah,'tanah')
```
dengan memasukkan parameter 
- list_of_dictionary = harga_rumah,dan 
- specified_key = 'tanah', 

akan menghasilkan:
```
['70', '70', '70', '100', '100', '100', '120', '120', '150', '150']
```


### 2. min_value(list_attributes) dan max_value(list_attributes):
Mengembalikan nilai value minimum dan maximum dari suatu key. Code:
``` code
    min_value(get_all_specified_attribute(harga_rumah,'tanah'))
    max_value(get_all_specified_attribute(harga_rumah,'tanah'))
```
dengan memasukkan parameter 
- list_attributes = get_all_specified_attribute(harga_rumah,'tanah'), 
akan menghasilkan nilai minimum dan maksimum dari key 'tanah' seperti berikut:

```
min value dari "tanah": 70
max value dari "tanah": 150
```

### 3. transform_attribute(attr,max_attr,min_attr):
Mengembalikan nilai transformasi dari sebuah nilai yang diinginkan. Rumus nilai transformasi adalah (x-min value)/(max value-min value) dimana x (parameter attr) adalah suatu angka (yang diinginkan), max value (parameter max_attr) adalah nilai/value terbesar dari suatu key, dan min value (paramater min_attr) adalah nilai/value terkecil dari suatu key. Code:
```
    transform_attribute(75,max_value(get_all_specified_attributes(harga_rumah,'tanah')),min_value(get_all_specified_attributes(harga_rumah,'tanah'))))
    
```
akan menghasilkan nilai transformasi sebesar:
```
    0.0625
```
untuk key 'tanah' dengan parameter:
- attr= 75, 
- max_attr= max_value(get_all_specified_attribute(harga_rumah,'tanah')), dan 
- min_attr = min_value(get_all_specified_attribute(harga_rumah,'tanah')).


### 4. data_transformation(list_of_dictionary, list_attribute_names):
Mengembalikan tuple berisi list of dictionary dan sebuah dictionary yang berisi nilai maksimum dan minimum dari masing-masing key. Code:
``` 
    data_transformation(harga_rumah,['tanah','bangunan','jarak_ke_pusat'])
```
akan mengasilkan tuple:
```
([{'tanah': 0.0, 'bangunan': 0.0, 'jarak_ke_pusat': 0.0, 'harga': '500'}, {'tanah': 0.0, 'bangunan': 0.2, 'jarak_ke_pusat': 0.375, 'harga': '400'}, {'tanah': 0.0, 'bangunan': 0.2, 'jarak_ke_pusat': 1.0, 'harga': '300'}, {'tanah': 0.375, 'bangunan': 0.0, 'jarak_ke_pusat': 0.375, 'harga': '700'}, {'tanah': 0.375, 'bangunan': 0.4, 'jarak_ke_pusat': 0.25, 'harga': '1000'}, {'tanah': 0.375, 'bangunan': 0.4, 'jarak_ke_pusat': 0.875, 'harga': '650'}, {'tanah': 0.625, 'bangunan': 1.0, 'jarak_ke_pusat': 0.125, 'harga': '2000'}, {'tanah': 0.625, 'bangunan': 0.6, 'jarak_ke_pusat': 0.875, 'harga': '1200'}, {'tanah': 1.0, 'bangunan': 1.0, 'jarak_ke_pusat': 0.875, 'harga': '1800'}, {'tanah': 1.0, 'bangunan': 0.8, 'jarak_ke_pusat': 0.0, 'harga': '3000'}], 

{'tanah': {'max': 150, 'min': 70}, 'bangunan': {'max': 100, 'min': 50}, 'jarak_ke_pusat': {'max': 55, 'min': 15}})

```
untuk parameter:
- data_transformation = harga_rumah, dan
- list_attribute_names = ['tanah','bangunan','jarak_ke_pusat'].

### 5. transform_data(data,attr_info):
Mengembalikan dictionary berisi masing-masing key dengan nilai value yang sudah ditransformasi. Code:
```
# assign harga_rumah dan attr_info dengan fungsi data_transformation untuk mendapatkan list of dict harga rumah dan attr info:

harga_rumah, attr_info = data_transformation(harga_rumah,)



# assign variabel 'data' dengan sebuah dictionary berisi key value yang diinginkan kemudian assign kembali variabel data dengan fungsi transform_data() untuk mendapatkan nilai value transformasi :

data = {'tanah':110,'bangunan':80,'jarak_ke_pusat':35} 
data = transform_data(harga_rumah,attr_info)



# jalankan fungsi transform data:

transform_data(data,attr_info)
```
akan menghasilkan data (dictionary dengan value nilai transformasi):
```
{'tanah': 0.5, 'bangunan': 0.6, 'jarak_ke_pusat': 0.5}

```

### 6. price_based_on_similarity()
Mengembalikan nilai 'harga' dari perbandingan terkecil antara masing-masing nilai asli dari key dengan masing-masing nilai transformasi dari key. Code:
```
harga = price_based_on_similarity(data,harga_rumah)
```
akan menghasilkan nilai harga sebesar:
```
    1200
```
untuk data:
```
{'tanah':110,'bangunan':80,'jarak_ke_pusat':35} 
```
