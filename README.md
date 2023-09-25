### Thaariq Kurnia Spama - 2206082801 - PBP F


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
1. Buatlah akun `Adaptable.io` menggunakan akun GitHub yang digunakan untuk membuat proyek shopping_list.
2. Jika sudah login, silakan tekan tombol `New App`. Pilih `Connect an Existing` Repository.
3. Hubungkan Adaptable.io dengan GitHub dan pilih `All Repositories` pada proses instalasi.
4. Pilihlah repositori proyek `inventory-cafe` sebagai basis aplikasi yang akan di-deploy. Pilih branch yang ingin dijadikan sebagai deployment branch.
5. Pilihlah `Python App Template` sebagai template deployment.
6. Pilih `PostgreSQL` sebagai tipe basis data yang akan digunakan.
7. Sesuaikan versi Python dengan spesifikasi aplikasimu. Untuk mengeceknya, nyalakan virtual environment dan jalankan perintah ```python --version.```
8. Pada bagian Start Command masukkan perintah ``` python manage.py migrate && gunicorn inventory_list.wsgi. ```
9. Masukkan nama aplikasi yang juga akan menjadi nama domain situs web aplikasimu.
10. Centang bagian `HTTP Listener on PORT` dan klik `Deploy App` untuk memulai proses deployment aplikasi.

## 2. Buatlah bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara urls.py, views.py, models.py, dan berkas html.
![Bagan Thaariq](bagan-thaariq.png)
- Client mengirimkan permintaan (HTTP Request) melalui browser untuk mengakses halaman web.
- Permintaan ini diteruskan ke sistem routing yang dikelola oleh Django, yang mencari pola URL yang cocok dengan permintaan tersebut.
- Setelah menemukan pola URL yang cocok, Django akan memanggil fungsi yang terkait dalam berkas views.py.
- Di dalam berkas views.py, kita dapat menjalankan alur aplikasi dan operasi basis data sesuai dengan arsitektur yang telah didefinisikan dalam models.py.
- Setelah semua operasi selesai, fungsi yang sesuai dalam berkas views.py akan menghasilkan halaman web yang diminta oleh client dalam format HTML, yang juga dapat disebut sebagai template.
- Berkas HTML ini akan disimpan dalam direktori "templates" untuk penggunaan selanjutnya.
- Terakhir, browser client akan merender berkas HTML ini sebagai tanggapan (HTTP Response) dari server Django, sehingga menghasilkan tampilan yang dapat dilihat oleh pengguna.


## 3. Jelaskan mengapa kita menggunakan virtual environment? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan virtual environment?
Kita tetap dapat membuat aplikasi tanpa menggunakan virtual environment tetapi sangat tidak disarankan karena tanpa virtual environment nantinya akan menghadapi masalah seperti konflik dependensi dengan proyek lain atau mengalami kesulitan dalam manajemen dependensi dan versi.

## 4. Jelaskan apakah itu MVC, MVT, MVVM dan perbedaan dari ketiganya.
MVC atau biasa disebut Model View Controller adalah sebuah metode untuk membuat sebuah aplikasi dengan memisahkan data dari tampilan dan cara bagaimana memprosesnya
MVT atau biasa disebut Model View Template merupakan pola arsitektur yang serupa dengan MVC, namun memiliki perbedaan pada bagaimana tampilan dihasilkan.
MVMM atau biasa disebut Model View ViewModel merupakan turunan dari pola desain arsitektrur MVC dan berfokus pada peningkatan logika presentasi

Perbedaan ketiganya yaitu terletak pada komponennnya yang berbeda. Pada MVC menggunakan Controller untuk mengatur alur Model dan View. MVT menggunakan Template untuk mengatur tampilan HTML. Dan MVVM menggunakan ViewModel untuk menghubungkan tampilan dengan data melalui pembaruan Model.


### Tugas 3
## 1. Apa perbedaan antara form POST dan form GET dalam Django?
POST	             
- Nilai variabel tidak ditampilkan di URL   
- Lebih aman
- Tidak dibatasi panjang string	           
- Pengambilan variabel dengan request.POST.get   
- Biasanya untuk input data melalui form	       
- Digunakan untuk mengirim data-data penting seperti password	                            

GET    
- Nilai variabel ditampilkan di URL sehingga user dapat dengan mudah memasukkan nilai variabel baru
- Kurang aman
- Dibatasi panjang string sampai 2047 karakter
- Pengambilan variabel dengan request.POST.get
- Biasanya untuk input data melalui link
- Digunakan untuk mengirim data-data tidak penting

## 2. Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengirim data?
XML digunakan untuk menyimpan dan mengirim data terstruktur.
JSON digunakan untuk pertukaran data yang sederhana, terutama dalam hal aplikasi web
HTML digunakan untuk membuat struktur dan tampilan halaman web, bukan untuk pertukaran data
Dapat disimpulkan bahwa XML dan JSON digunakan untuk pertukaran data, sementara HTML digunakan untuk mengatur tampilan dan struktur konten halaman web.

## 3. Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?
Karena JSON memiliki banyak keuntungan seperti lebih ringan,lebih cepat dan lebih sederhana dari segi sintaksisnya dibandingkan dengan XML. Untuk itu JSON memungkinkan pengembang dapat mengirim, menerima dan meproses data dari berbagai jenis aplikasi dengan cepat dan mudah
## 4. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).

### Membuat input form untuk menambahkan objek model pada app sebelumnya.
Untuk membuat input form dengan membuat berkas baru pada direktori `main` dengan nama forms.py dan tambahkan kode berikut 
```python
from django.forms import ModelForm
from main.models import Product

class ProductForm(ModelForm):
    class Meta:
        model = Product
        fields = ["name", "amount", "description"]
```
kemudian buka berkas `views.py` pada folder main dan tambahkan beberapa import berikut
```python
from django.http import HttpResponseRedirect
from main.forms import ProductForm
from django.urls import reverse
```
Selanjutnya buat fungsi baru dengan nama `create_product` pada berkas tersebut untuk menerima parameter `request`dan isi fungsi tersebut dengan kode berikut untuk menghasilkan formulir yang memungkinkan pengguna untuk menambahkan data produk secara otomatis saat data tersebut di-submit melalui formulir.
```python
def create_product(request):
    form = ProductForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        form.save()
        return HttpResponseRedirect(reverse('main:show_main'))

    context = {'form': form}
    return render(request, "create_product.html", context)
```
Ubah fungsi `show_main` pada berkas views.py menjadi seperti berikut
```python
def show_main(request):
    products = Product.objects.all()

    context = {
        'name': 'Pak Bepe', # Nama kamu
        'class': 'PBP A', # Kelas PBP kamu
        'products': products
    }
    return render(request, "main.html", context)
```
Import fungsi `create_product` pada berkas `urls.py` di folder main
```python
from main.views import show_main, create_product
```
Tambahkan path URL ke dalam bagian `urlpatterns` pada berkas `urls.py` di direktori "main" untuk mengakses fungsi yang sudah di-import sebelumnya
```python
path('create-product', create_product, name='create_product'),
```
Buat berkas HTML baru dengan nama `create_product.html` pada direktori `main/templates`. Isi `create_product.html` dengan kode berikut.
```html
{% extends 'base.html' %} 

{% block content %}
<h1>Add New Product</h1>

<form method="POST">
    {% csrf_token %}
    <table>
        {{ form.as_table }}
        <tr>
            <td></td>
            <td>
                <input type="submit" value="Add Product"/>
            </td>
        </tr>
    </table>
</form>

{% endblock %}
```
Tambahkan kode berikut di dalam `{% block content %}` di `main.html` untuk menampilkan data produk dalam bentuk table serta tombol "Add New Product" yang akan redirect ke halaman form.
```html
...
<table>
    <tr>
        <th>Name</th>
        <th>Price</th>
        <th>Description</th>
        <th>Date Added</th>
    </tr>

    {% comment %} Berikut cara memperlihatkan data produk di bawah baris ini {% endcomment %}

    {% for product in products %}
        <tr>
            <td>{{product.name}}</td>
            <td>{{product.price}}</td>
            <td>{{product.description}}</td>
            <td>{{product.date_added}}</td>
        </tr>
    {% endfor %}
</table>

<br />

<a href="{% url 'main:create_product' %}">
    <button>
        Add New Product
    </button>
</a>

{% endblock content %}
```
### Tambahkan 5 fungsi views untuk melihat objek yang sudah ditambahkan dalam format HTML, XML, JSON, XML by ID, dan JSON by ID.
Buat 5 fungsi views pada berkas `views.py` di direktori main dengan kode sebagai berikut
```python
def create_product(request):
    form = ProductForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        form.save()
        return HttpResponseRedirect(reverse('main:show_main'))

    context = {'form': form}
    return render(request, "create_product.html", context)

def show_xml(request):
    data = Product.objects.all()
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json(request):
    data = Product.objects.all()
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")

def show_xml_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```
### Membuat routing URL untuk masing-masing views yang telah ditambahkan pada poin 2.
Buka `urls.py` pada folder main dan import fungsi yang telah ditambahkan pada poin 2
```python
from main.views import create_product, show_xml, show_json, show_xml_by_id, show_json_by_id 
```
Kemudian tambahkan path url ke dalam `urlpatterns` untuk mengakses fungsi yang sudah diimport tadi
```python
...
    path('create-product', create_product, name='create_product'),
    path('xml/', show_xml, name='show_xml'), 
    path('json/', show_json, name='show_json'), 
    path('xml/<int:id>/', show_xml_by_id, name='show_xml_by_id'),
    path('json/<int:id>/', show_json_by_id, name='show_json_by_id'),
...
```
### Tugas 4
## Apa itu Django UserCreationForm, dan jelaskan apa kelebihan dan kekurangannya?
formulir yang disediakan dari DJango unutk mempermudah pengelolaan pengguna user dalam aplikasi web. Kelebihannya itu mudah digunakan, kustomisasi dan kompatibilitas dengan model pengguna. Kekurangannya itu karena terbatas pada model user bawaan, tampilan standar dan kurangnya fitur khusus.

## Apa perbedaan antara autentikasi dan otorisasi dalam konteks Django, dan mengapa keduanya penting?
Autentikasi merupakan proses verifikasi identitas pengguna. Autentikasi membantu melindungi suatu aplikasi dari akses yang tidak sah dengan memastikan bahwa hanya pengguna yang sah yang dapat masuk
Otorisasi merupakan tindakan memberi izin kepada pihak yang diautentikasi untuk melakukan sesuatu. Otorisasi membantu melindungi suatu aplikasi dengan memastikan bahwa pengguna hanya dapat melakukan tindakan yang mereka izinkan, dan ini memungkinkan untuk mengelola hak akses secara efisien.
Keduanya penting karena sama-sama untuk menjaga keamanan aplikasi web

## Apa itu cookies dalam konteks aplikasi web, dan bagaimana Django menggunakan cookies untuk mengelola data sesi pengguna?
Cookies adalah file teks yang menyimpan data kecil untuk mengidentifikasi komputer saat menggunakan jaringan komputer. Dalam konteks aplikasi web, Django menggunakan cookies untuk mengelola data sesi pengguna. Django menyediakan fitur session framework yang memungkinkan pengguna untuk menyimpan data sesi di dalam cookies. Data sesi ini dapat digunakan untuk menyimpan informasi seperti preferensi pengguna, keranjang belanja, riwayat penelusuran, dan lain-lain.

## Apakah penggunaan cookies aman secara default dalam pengembangan web, atau apakah ada risiko potensial yang harus diwaspadai?
Cookies dapat digunakan secara aman dalam pengembangan web, tetapi diperlukan perhatian terhadap praktik keamanan yang baik dan implementasi yang benar untuk meminimalkan risiko. Penting untuk selalu mengikuti pedoman keamanan web terkini dan melakukan audit keamanan secara berkala untuk mengidentifikasi potensi risiko dan mengatasinya secepat mungkin.

## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).

### Mengimplementasikan fungsi registrasi, login, dan logout untuk memungkinkan pengguna untuk mengakses aplikasi sebelumnya dengan lancar.
# Fungsi registrasi
Buat fungsi bernama `register` pada `views.py` di subdirektori `main` yang berisi code seperti berikut.
```python
def register(request):
    form = UserCreationForm()

    if request.method == "POST":
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            messages.success(request, 'Your account has been successfully created!')
            return redirect('main:login')
    context = {'form':form}
    return render(request, 'register.html', context)
```
Tambahkan import `redirect`,`UserCreationForm`, dan `messages` 
```python
from django.shortcuts import redirect
from django.contrib.auth.forms import UserCreationForm
from django.contrib import messages  
```
Buat berkas HTML baru dengan nama `register.html` pada folder `main/templates` yang berisi berikut.
```html
{% extends 'base.html' %}

{% block meta %}
    <title>Register</title>
{% endblock meta %}

{% block content %}  

<div class = "login">
    
    <h1>Register</h1>  

        <form method="POST" >  
            {% csrf_token %}  
            <table>  
                {{ form.as_table }}  
                <tr>  
                    <td></td>
                    <td><input type="submit" name="submit" value="Daftar"/></td>  
                </tr>  
            </table>  
        </form>

    {% if messages %}  
        <ul>   
            {% for message in messages %}  
                <li>{{ message }}</li>  
                {% endfor %}  
        </ul>   
    {% endif %}

</div>  

{% endblock content %}
```
Impor fungsi yang sudah dibuat sebelumnya dan tambahkan path url ke dalam `urlpatterns` di berkas `urls.py` pada subdirektori `main`
```python
from main.views import register
```
```python
...
path('register/', register, name='register'),
```

# Fungsi Login
Buat fungsi bernama `register` pada `views.py` di subdirektori `main` yang berisi code seperti berikut.
```python
def login_user(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('main:show_main')
        else:
            messages.info(request, 'Sorry, incorrect username or password. Please try again.')
    context = {}
    return render(request, 'login.html', context)
```
Tambahkan import `authenticate`, dan `login` 
```python
from django.contrib.auth import authenticate, login
```
Buat berkas HTML baru dengan nama `login.html` pada folder `main/templates` yang berisi berikut.
```html
{% extends 'base.html' %}

{% block meta %}
    <title>Login</title>
{% endblock meta %}

{% block content %}

<div class = "login">

    <h1>Login</h1>

    <form method="POST" action="">
        {% csrf_token %}
        <table>
            <tr>
                <td>Username: </td>
                <td><input type="text" name="username" placeholder="Username" class="form-control"></td>
            </tr>
                    
            <tr>
                <td>Password: </td>
                <td><input type="password" name="password" placeholder="Password" class="form-control"></td>
            </tr>

            <tr>
                <td></td>
                <td><input class="btn login_btn" type="submit" value="Login"></td>
            </tr>
        </table>
    </form>

    {% if messages %}
        <ul>
            {% for message in messages %}
                <li>{{ message }}</li>
            {% endfor %}
        </ul>
    {% endif %}     
        
    Don't have an account yet? <a href="{% url 'main:register' %}">Register Now</a>

</div>

{% endblock content %}
```
Impor fungsi yang sudah dibuat sebelumnya dan tambahkan path url ke dalam `urlpatterns` di berkas `urls.py` pada subdirektori `main`
```python
from main.views import login_user
```
```python
...
path('login/', login_user, name='login'),
```

# Fungsi Logout
Buat fungsi bernama `logout_user` pada `views.py` di subdirektori `main` yang berisi code seperti berikut.
```python
def logout_user(request):
    logout(request)
    return redirect('main:login')
```
Tambahkan import `redirect`,`UserCreationForm`, dan `messages` 
```python
from django.contrib.auth import logout
```
Tambahkan potongan kode berikut setelah hyperlink tag untuk Add New Product pada berkas `main.html`
```html
...
<a href="{% url 'main:logout' %}">
    <button>
        Logout
    </button>
</a>
...
```
Impor fungsi yang sudah dibuat sebelumnya dan tambahkan path url ke dalam `urlpatterns` di berkas `urls.py` pada subdirektori `main`
```python
from main.views import logout_user
```
```python
...
path('logout/', logout_user, name='logout'),
```
### Membuat dua akun pengguna dengan masing-masing tiga dummy data menggunakan model yang telah dibuat pada aplikasi sebelumnya untuk setiap akun di lokal.
akun pertama
![Akun Rapunzz](rapunzz.jpg)
akun kedua
![Akun Spama](spama.jpg)

### Menghubungkan model Item dengan User.
Tambahkan code berikut untuk mengimpor model pada berkas `models.py` di subdirektori `main`
```python
...
from django.contrib.auth.models import User
...
```
Pada model `product` yang sudah ada ,tambahkan kode berikut.
```python
class Product(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    ...
```
Ubah fungsi `create_product` pada berkas `views.py` di subdirektori `main`
```python
def create_product(request):
 form = ProductForm(request.POST or None)

 if form.is_valid() and request.method == "POST":
     product = form.save(commit=False)
     product.user = request.user
     product.save()
     return HttpResponseRedirect(reverse('main:show_main'))
 ...
 ```
 dan ubah fungsi `show_main` juga 
 ```python
 def show_main(request):
    products = Product.objects.filter(user=request.user)

    context = {
        'name': request.user.username,
    ...
...
```
Lakukan migrasi model  dengan perintah `python manage.py makemigrations` pada terminal, Kemudian pilih `1`  untuk menetapkan default value untuk field user pada semua row yang telah dibuat pada basis data. dan pilih `1` lagi untuk  menetapkan user dengan ID 1 (yang sudah kita buat sebelumnya) pada model yang sudah ada.

Terakhir, lakukan `python manage.py migrate` untuk mengaplikasikan migrasi yang dilakukan pada poin sebelumnya.

### Menampilkan detail informasi pengguna yang sedang logged in seperti username dan menerapkan cookies seperti last login pada halaman utama aplikasi.
Informasi Pengguna
![Informasi User](last_login.jpg)
