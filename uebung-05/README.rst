==============================================================================
Übung 5: High Performance Setups mit Buildout
==============================================================================

Einfaches High-Performance Setup::


                     NGINX (Port 80)
                           |
                           |
                   VARNISH (Port 8088)
                           |
                           |
                   HAPROXY (Port 8080)
                           |
                           |
              +------------+------------+
              |                         |
    INSTANZ 1 (Port 8081)     INSTANZ 2 (Port 8082)
              |                         |
              +------------+------------+
                           |
                           |
                    ZEO (Port 8089)

Komponenten:

- Nginx (Frontend Webserver)
- Varnish (Reverse-Proxy Caching Server)
- HAProxy (Load Balancer)
- Plone Instanzen
- ZEO (Verteilter Python Objekt-Storage)


Vorbereitungen
--------------

Varnish System-Abhängigkeiten installieren::

  $ sudo apt-get install libpcre3-dev


Buildout
--------

Kern Buildout (buildout.d/core.cfg):

.. literalinclude:: ../../uebung-05/buildout.d/core.cfg

Entwicklungs-Buildout (buildout.cfg):

.. literalinclude:: ../../uebung-05/buildout.cfg


Deployment Buildout
-------------------

Kern Deployment Buildout (buildout.d/deployment.cfg):

.. literalinclude:: ../../uebung-05/buildout.d/deployment.cfg

Deployment Buildout (deployment.cfg):

.. literalinclude:: ../../uebung-05/deployment.cfg

Staging Buildout (staging.cfg):

.. literalinclude:: ../../uebung-05/staging.cfg

Supervisor
----------

Supervisor starten::

  $ bin/supervisord

Supervisor Status:

  $ bin/supervisorctl status
  haproxy                          RUNNING   pid 12587, uptime 0:01:18
  instance1                        RUNNING   pid 12590, uptime 0:01:18
  instance2                        RUNNING   pid 12591, uptime 0:01:18
  instance3                        RUNNING   pid 12592, uptime 0:01:18
  instance4                        RUNNING   pid 12593, uptime 0:01:18
  varnish                          RUNNING   pid 12588, uptime 0:01:18
  zeo                              RUNNING   pid 12589, uptime 0:01:18

Supervisor Stop:

  $ bin/supervisorctl stop all
  haproxy: stopped
  varnish: stopped
  zeo: stopped
  instance1: stopped
  instance2: stopped
  instance3: stopped
  instance4: stopped

Supervisor Start:

  $ bin/supervisorctl start all
  haproxy: started
  varnish: started
  zeo: started
  instance1: started
  instance2: started
  instance3: started
  instance4: started

Supervisort Herunterfahren:

  $ bin/supervisorctl shutdown

HAProxy Load Balancer
---------------------

Gehe auf: http://localhost:8087/haproxy-status


.. image:: _images/haproxy.png

Instanz 4 stoppen:

  $ bin/supervisorctl stop instance4

Varnish
-------

Gehe auf: http://localhost:8081/Plone (Plone Instanz 1 ohne Varnish)

HTTP Header:

.. image:: _images/plone-without-varnish.png

Gehe auf: http://localhost:8080/Plone (Varnish mit Load Balancing Setup)

HTTP Header:

.. image:: _images/varnish.png


plone.app.caching
-----------------

Damit Varnish richtig funktioniert sollte plone.app.caching eingerichtet werden.

HTTP Header:

.. image:: _images/varnish-with-plone-app-caching.png


Aufgabe
-------

Erstelle eine weitere Konfiguration für einen development Server (dev.cfg).
