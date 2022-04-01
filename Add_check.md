# Thêm crontab Check

VD: Thêm một crontab monitor với các thông tin:
<ul>
 <ul>
<li> name check: Backup System
<li> tag: backup
<li> description: Test
<li> schedule: Kiểu Cron schedule ( Mỗi 60 phút, với Grace time là 10 phút )
<li> notification Method: Telgram và Mail quynv.vccloud.vn
</ul>
 </ul>

### 1.1 Tạo Check
- Đăng nhập vào healcheck.io, chọn `project > add check`

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/33.png" />

### 1.2 Add Name,tag ,Description cho Check

- Chọn `edit`  để thêm name, tag, description

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/39.png" />

- Nhập thông tin

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/34.png" />

### 1.3 Thêm Schedule

- Click `Change Schedule > Cron` và thêm thông tin

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/36.png" />


### 1.4 Chọn Notification Methods

- Ở `Notification Methods` chọn phương thức cảnh báo

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/37.png" />

### 1.5 Lấy URL Ping

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/38.png" />

### 1.6 Cấu hình Crontab trên máy cần monitor

- Thêm Crontab với định dạng:
```sh
 <Cron Expression> <curl Ping Status Start> ; <script> && <curl Ping status Success>
```
- VD:

```sh
root@quynv:~# crontab -e

* * * * * curl -m 10 --retry 3 http://10.5.9.214:8000/ping/5b484358-fb2d-488e-b77b-cef02a267350/start ; /root/b&& curl -m 10 --retry 3 http://10.5.9.214:8000/ping/5b484358-fb2d-488e-b77b-cef02a267350
```


