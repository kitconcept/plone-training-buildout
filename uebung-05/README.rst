
Varnish:

sudo apt-get install libpcre3-dev


NGINX (Port 80)
  |
VARNISH (Port 8080)
  |
HAPROXY (Port 8081)
  |
  +------------+----------+----------+
  |            |          |          |
Instanz 1  Instanz 2  Instanz 3  Instanz 4
  |            |          |          |
  +------------+----------+----------+
  |
ZEO (8089)


Varnish: plone.app.caching einrichten
