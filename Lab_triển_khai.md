# Mô hình

```sh
 
                       192.168.18.0/24 |
                        +----------------------------+
                        |                            |                                                     
                        |192.168.18.75               | 192.168.18.170                   
            +-----------+-----------+    +-----------+-----------+    
            |     [healthcheck]     |    |        [client]       |     
            |                       |    |                       |  
            |                       |    |                       |  
            |                       |    |                       |    
            |                       |    |                       |    
            |                       |    |                       |    
            +-----------+-----------+    +-----------------------+      
```

## Setting Up for Development

To set up Healthchecks development environment:

* Install dependencies (Debian/Ubuntu):
```sh
root@quynv:~sudo apt-get update
root@quynv:~ apt-get install -y gcc python3-dev python3-venv libpq-dev
```
* Prepare directory for project code and virtualenv. Feel free to use a
  different location:
```sh
 root@quynv:~ mkdir -p ~/webapps
 root@quynv:~ cd ~/webapps
```
* Prepare virtual environment
  (with virtualenv you get pip, we'll use it soon to install requirements):
```sh
 root@quynv:~/webapps# python3 -m venv hc-venv
 (hc-venv) root@quynv:~/webapps# source hc-venv/bin/activate
 (hc-venv) root@quynv:~/webapps# pip3 install wheel
```
* Check out project code:
```sh
(hc-venv) root@quynv:~/webapps# git clone https://github.com/healthchecks/healthchecks.git
```
* Install requirements (Django, ...) into virtualenv:
```sh
(hc-venv) root@quynv:~/webapps# pip install -r healthchecks/requirements.txt
```

* Create database tables and a superuser account:
```sh
 (hc-venv) root@quynv:~/webapps# cd ~/webapps/healthchecks
 (hc-venv) root@quynv:~/webapps/healthchecks# ./manage.py migrate
 (hc-venv) root@quynv:~/webapps/healthchecks# ./manage.py createsuperuser
```
 
* Run tests:
```sh
(hc-venv) root@quynv:~/webapps/healthchecks# ./manage.py test
```
* Run development server:
```sh
(hc-venv) root@quynv:~/webapps/healthchecks# nohup ./manage.py runserver 192.168.18.75:8000 &
```
The site should now be running at `http://192.168.18.75:8000`.

## Sending Status Notifications

healtchecks comes with a `sendalerts` management command, which continuously
polls database for any checks changing state, and sends out notifications as
needed. Within an activated virtualenv, you can manually run
the `sendalerts` command like so:
```sh
(hc-venv) root@quynv:~/webapps/healthchecks# nohup ./manage.py sendalerts &
```

## Sending Emails

Healthchecks must be able to send email messages, so it can send out login
links and alerts to users. Specify your SMTP credentials using the following
environment variables:

```python
(hc-venv) root@quynv-healthcheck:~/webapps/healthchecks# vim hc/settings.py


EMAIL_HOST = os.getenv("EMAIL_HOST", "smtp.gmail.com")
EMAIL_PORT = envint("EMAIL_PORT", "587")
EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER", "quy15091998@gmail.com")
EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD", "********")
EMAIL_USE_TLS = envbool("EMAIL_USE_TLS", "True")
EMAIL_USE_VERIFICATION = envbool("EMAIL_USE_VERIFICATION", "True")
```
### Telegram

B1: Tạo bot Telegram

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/01.png" />

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/02.png" />
B2: Lấy id group-chat, type-chat, tên group chat 
- Tạo group với bot và chat một câu bất kỳ để lấy id group chat, type-chat, tên group chat...
 
<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/04.png" />

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/05.png" />

- Lưu lại group-chat, type-chat, tên group chat

B3: Thêm tên bot và token bot telegram vào file configure

```python
(hc-venv) root@quynv-healthcheck:~/webapps/healthchecks# vim hc/settings.py


TELEGRAM_BOT_NAME = os.getenv("TELEGRAM_BOT_NAME", "croncheck45565_bot")
TELEGRAM_TOKEN = os.getenv("TELEGRAM_TOKEN", "5112644717:AAGq87TxNNv-qfXF8-aIkBmBAXRl-TCOfzA")
```
B4: Restart server healthcheck.io


B5: Add API channel
 - Truy cập vào trang admin `http://192.168.18.75:8000/admin/`
 - Đến  API -> Channel -> add
 - 
 <img src="https://github.com/lean15998/healthcheck.io/blob/main/images/06.png" />
 
 
 - Nhập các thông tin như sau:
 
<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/07.png" />

B6: Gửi một thông báo test đến group telegram

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/08.png" />

- Check thông báo trên telegram

<img src="https://github.com/lean15998/healthcheck.io/blob/main/images/09.png" />

