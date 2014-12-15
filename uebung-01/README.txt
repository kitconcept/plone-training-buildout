===============================================================================
Übung 1: Plone Installation
===============================================================================

In der ersten Übung lernen wir wie Plone installiert wird.


Drei Wege zur Installation von Plone
===============================================================================

Es gibt drei verschiedene Wege zur Installation von Plone:

  - `Unified Installer`_ (Linux, Mac OS X, Window)
  - Windows Installer (letzte Version 4.0.7)
  - Buildout

_`Unified Installer`:http://plone.org/products/plone/releases


Vorbereitungen
===============================================================================

Curl installieren::

  $ sudo apt-get install -y curl

Python 2.7 installieren::

  $ sudo apt-get install -y libxslt1-dev libxml2-dev
  $ sudo apt-get install -y python-dev python-imaging python-lxml

Distribute installieren::

  $ curl http://python-distribute.org/distribute_setup.py | sudo python


Buildout
===============================================================================

Plone Verzeichnis erstellen::

  $ mkdir uebung-01

Download bootstrap Datei::

  $ cd uebung-01
  $ curl -O http://python-distribute.org/bootstrap.py

Datei "buildout.cfg" erstellen::

  [buildout]
  parts = instance
  extends = http://dist.plone.org/release/4.2.1/versions.cfg

  [instance]
  recipe = plone.recipe.zope2instance
  http-address = 8080
  user = admin:admin
  eggs = Plone

Buildout ausführen::

  $ python bootstrap.py
  $ bin/buildout

Zope Instanz starten (im "Foreground"-Modus)::

  $ bin/instance fg

Zope Instanz starten::

  $ bin/instance start

Zope Instanz stoppen::

  $ bin/instance stop


Plone Demo
===============================================================================

- Plone Instanz erstellen
- Front-page editieren
- Ordner hinzufügen
- Seite hinzufügen
- Seite veröffentlichen
