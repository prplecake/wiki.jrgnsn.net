1. Clone project.
```sh
git clone https://github.com/prplecake/legacy.sr.ht
```
2. Create database and database user
```sql
CREATE DATABASE legacy.sr.ht;
CREATE USER srht WITH ENCRYPTED PASSWORD 'password';
GRANT ALL PRIVILEGES ON DATABASE legacy.sr.ht TO srht;
```
3. Create virtualenv
```sh
$ python3 -m virtualenv venv
$ source venv/bin/activate
```
4. Install python dependencies
```sh
$ pip install -r requirements.txt
```
5. Set up config</li>
```sh
$ cp alembic.ini.example alembic.ini
$ cp config.ini.example config.ini
$ $EDITOR alembic.ini
$ $EDITOR config.ini
```
6. Compile static assets
```sh
$ make
```
7. Install gunicorn
```sh
$ pip install gunicorn
```
8. Set up nginx config
```sh
$ sudo cp contrib/nginx.conf /etc/nginx/sites-available/legacy.sr.ht.conf
$ sudo $EDITOR /etc/nginx/sites-available/legacy.sr.ht.conf
$ sudo ln -s /etc/nginx/sites-available/legacy.sr.ht.conf /etc/nginx/sites-enabled
$ sudo nginx -t # test the config
$ sudo nginx -s reload
```
9. Run it!
```sh
$ gunicorn app:app -b 127.0.0.1:8000
```

At this point, you should be able to browse legacy.sr.ht on whatever domain you set up in nginx. Next steps would be to set this up as an init script or systemd service.
