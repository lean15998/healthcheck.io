#### Thông tin: Add crontab monitor : {check: ( name:backupsystem; tag:backup; description:Test )} a.sh thực hiện 1 tiếng 1 lần, grace time= 10p, bắn cảnh báo về telegram


## Tạo Check



## Add Name,tag ,Description cho Check

## Chọn kiểu Schedule và cấu hình Period time (Kiểu Simple Schedule) hoặc Cron Expression (Kiểu Cron Schedule), Server Time Zone (Kiểu Cron Schedule) và Grace Time

## Chọn Notification Methods

## Lấy URL Ping

## Cấu hình Crontab trên máy cần monitor

- Thêm Crontab với định dạng:
```sh
 <Cron Expression> <curl Ping Status Start> ; <script> && <curl Ping status Success>

```sh
root@quynv:~# crontab -e

* * * * * curl -m 10 --retry 3 http://10.5.9.214:8000/ping/5b484358-fb2d-488e-b77b-cef02a267350/start ; /root/a && curl -m 10 --retry 3 http://10.5.9.214:8000/ping/5b484358-fb2d-488e-b77b-cef02a267350
```


