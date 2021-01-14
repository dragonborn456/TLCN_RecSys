# Cách cài đặt demo
Thực nghiệm các thuật toán liên quan tới 1 hệ thống gợi ý phim qua demo sau

Dataset: https://github.com/sidooms/MovieTweetings
API: https://www.themoviedb.org


## Tiến hành cài đặt

### Tải Python mới nhất( 3.x)
 
Sử dụng Anaconda có thể bỏ qua bước này

## Tải source code
Tải file source code .zip này về máy

## Create a virtual environment for the project

Tạo môi trường ảo để thực thi các lệnh cài đặt cho demo. Tên môi trường ảo của mình là prs( có thể thay đổi tùy ý)

*   Anaconda 
    > cd moviegeek
    > conda create -n prs python=3.6( thay đổi theo phiên bản python của bạn)
    > conda activate prs

### Tải các package
2 bước để tải các pakage
*   *requirements.txt* 


    ```bash
    > for /f %i in (requirements.txt) do conda install --yes %i
    ```
*   *codepackage.txts*
Chạy từng dòng lệnh ở codepackage.txt
    
## Thiết lập database

####  Cài đặt  PostGreSQL
https://www.postgresql.org/download/


#### Create the database for MovieGEEK 
Sau khi cài đặt PostGreSQL, chạy pgadmin4 để tiến hành tạo database. Đặt tên database là moviegeek. Tạo Username và Password( rất cần thiết cho bước tiếp theo) 

ng these [instructions](https://www.psycopg.org/docs/install.html). 

####  Configure the Django database connection to connect to PostGreSql

Mở file sau trong thư mục moviegeek

`prs_project/settings.py` 

Tiến hành cập nhật các thông tin sau:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'moviegeek',                      
        'USER': 'db_user',
        'PASSWORD': 'db_user_password',
        'HOST': 'db_host',
        'PORT': 'db_port_number',
    }
}
```
Update the USER, PASSWORD
* USER(db_user): Tên Username đã tạo ở trên
* PASSWORD(db_user_password): Password đã tạo ở trên



#### Create the MovieGEEKS databases
Tiến hành migrate các model của django vào PostgreSQL qua các lệnh sau:

```bash
> python manage.py makemigrations
> python manage.py migrate --run-syncdb
```

#### Populate database 
Chạy các file sau để lấy dữ liệu về PostgreSQL
```bash
> python populate_moviegeek.py
> python populate_ratings.py
```

### Chạy các mô hình cho các thuật toán
Chạy lần lượt các file sau: lda_model_calculator.py -> item_similarity_calculator.py -> matrix_factorization_calculator.py cho Content-based, Item-Item CF và SVD

### Khởi động web
Chạy lệnh sau:
```bash
> python manage.py runserver 127.0.0.1:8000
```
Có thể sử dụng port khác ngoài 8000

## Tắt kết  nối
Ctrl + C
Sau đó tắt môi trường ảo

```bash
> conda deactivate
```


