## 1. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
### Membuat sebuah proyek Django baru.
Langkah pertama yang saya lakukan adalah membuat direktori baru dengan nama yang diinginkan seperti "inventory_list" kemudian membuat command prompt di dalam direktori tersebut, kemudian membuat virtual environment dan mengaktifkannya. Langkah kedua membuat berkas requirements.txt pada direktori yang sama pada sebelumnya dan ditambahkan dependenciesnya. Kemudian pasang dependencies dan buat proyek Django dengan nama yang diinginkan sebelumnya seperti "inventory_list" dengan perintah ``` django-admin startproject inventory_list . ```  . Jangan lupa untuk menambahkan "*" pada ALLOWED_HOSTS di settings.py untuk keperluan deployment dan unggah proyek ke repository github. Dengan begini sebuah proyek Django baru telah berhasil dibuat.
### Membuat aplikasi dengan nama main pada proyek tersebut.
Untuk Membuat aplikasi dengan nama main, langkah yang diperlukan yang pertama yaitu menjalankan perintah "python manage.py startapp main" pada proyek inventory_list untuk membuat aplikasi baru. Kemudian mendaftarkan aplikasi main ke dalam proyek dengan urutannya yaitu membuka berkas settings.py di dalam direktori proyek shopping_list kemudian temukan variabel INSTALLED_APPS dan Tambahkan 'main' ke dalam daftar INSTALLED_APPS
### Melakukan routing pada proyek agar dapat menjalankan aplikasi main.
Melakukan routing pada proyek agar dapat menjalankan aplikasi main yaitu mengedit berkas urls.py pada direktori inventory_list dan impor fungsi include dari django.urls
```python
from django.urls import path, include
```
Kemudian tambahkan rute URL seperti berikut untuk mengarahkan ke tampilan main di dalam variabel urlpatterns.
```python
urlpatterns = [
    ...
    path('main/', include('main.urls')),
]
```

### Membuat model pada aplikasi main dengan nama Item dan memiliki atribut wajib sebagai berikut.
    name sebagai nama item dengan tipe CharField.
    amount sebagai jumlah item dengan tipe IntegerField.
    description sebagai deskripsi item dengan tipe TextField.

Untuk membuat model pada aplikasi main dengan nama Item dan memiliki atribut wajib, langkah pertama yaitu buka berkas models.py pada direktori aplikasi main dan isi berkas tersebut dengan kode 
```python
from django.db import models
class Product(models.Model):
    name = models.CharField(max_length=255)
    date_added = models.DateField(auto_now_add=True)
    amount = models.IntegerField()
    description = models.TextField()
```
### Membuat sebuah fungsi pada views.py untuk dikembalikan ke dalam sebuah template HTML yang menampilkan nama aplikasi serta nama dan kelas kamu.
Membuat sebuah fungsi pada views.py untuk dikembalikan ke dalam sebuah template HTML. Buka berkas views.py yang terletak di dalam berkas aplikasi main, tambahkan baris-baris import berikut di bagian paling atas berkas
```python
from django.shortcuts import render
```
kemudian tambahkan fungsi show_main dibawah impor :
```python
def show_main(request):
    context = {
        'name': 'Pak Bepe',
        'class': 'PBP A'
    }

    return render(request, "main.html", context)
```
### Membuat sebuah routing pada urls.py aplikasi main untuk memetakan fungsi yang telah dibuat pada views.py.
Membuat sebuah routing pada urls.py aplikasi main untuk memetakan fungsi yang telah dibuat pada views.py. Buat berkas urls.py didalam direktori main dan isi dengan kode berikut.
```python
from django.urls import path
from main.views import show_author

app_name = 'main'

urlpatterns = [
    path('', show_author, name='show_author'),
]
```
### Melakukan deployment ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.
Sebelum melakukan deployment, perlu melakukan perintah python manage.py runserver
kemudian buka http://localhost:8000/main jika berhasil, bisa mulai proses deployment pada adaptable.
    1. Buatlah akun Adaptable.io menggunakan akun GitHub yang digunakan untuk membuat proyek shopping_list.
    2. Jika sudah login, silakan tekan tombol New App. Pilih Connect an Existing Repository.
    3. Hubungkan Adaptable.io dengan GitHub dan pilih All Repositories pada proses instalasi.
    4. Pilihlah repositori proyek inventory-cafe sebagai basis aplikasi yang akan di-deploy. Pilih branch yang ingin dijadikan sebagai deployment branch.
    5. Pilihlah Python App Template sebagai template deployment.
    6. Pilih PostgreSQL sebagai tipe basis data yang akan digunakan.
    7. Sesuaikan versi Python dengan spesifikasi aplikasimu. Untuk mengeceknya, nyalakan virtual environment dan jalankan perintah python --version.
    8. Pada bagian Start Command masukkan perintah ``` python manage.py migrate && gunicorn inventory_list.wsgi. ```
    9. Masukkan nama aplikasi yang juga akan menjadi nama domain situs web aplikasimu.
    10. Centang bagian HTTP Listener on PORT dan klik Deploy App untuk memulai proses deployment aplikasi.

## 2. Buatlah bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara urls.py, views.py, models.py, dan berkas html.


## 3. Jelaskan mengapa kita menggunakan virtual environment? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan virtual environment?
Kita tetap dapat membuat aplikasi tanpa menggunakan virtual environment tetapi sangat tidak disarankan karena tanpa virtual environment nantinya akan menghadapi masalah seperti konflik dependensi dengan proyek lain atau mengalami kesulitan dalam manajemen dependensi dan versi.

## 4. Jelaskan apakah itu MVC, MVT, MVVM dan perbedaan dari ketiganya.
MVC atau biasa disebut Model View Controller adalah sebuah metode untuk membuat sebuah aplikasi dengan memisahkan data dari tampilan dan cara bagaimana memprosesnya
MVT atau biasa disebut Model View Template merupakan pola arsitektur yang serupa dengan MVC, namun memiliki perbedaan pada bagaimana tampilan dihasilkan.
MVMM atau biasa disebut Model View ViewModel merupakan turunan dari pola desain arsitektrur MVC dan berfokus pada peningkatan logika presentasi

Perbedaan ketiganya yaitu terletak pada komponennnya yang berbeda. Pada MVC menggunakan Controller untuk mengatur alur Model dan View. MVT menggunakan Template untuk mengatur tampilan HTML. Dan MVVM menggunakan ViewModel untuk menghubungkan tampilan dengan data melalui pembaruan Model.