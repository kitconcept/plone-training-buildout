==============================================================================
Übung 1: Buildout Basics
==============================================================================

In der ersten Übung lernen wir, wie Plone mit Hilfe von Buildout installiert wird.


Drei Wege zur Installation von Plone
==============================================================================

Es gibt drei verschiedene Wege zur Installation von Plone:

  - `Unified Installer`_ (Linux, Mac OS X, Window)
  - Windows Installer (letzte Version 4.0.7)
  - Buildout

_`Unified Installer`:http://plone.org/products/plone/releases

.. note::

  Wir konzentrieren uns auf die Variante mit Buildout. Diese wird auch vom Unified Installer verwendet.


Vorbereitungen (Ubuntu 14.04 LTS)
==============================================================================

Curl installieren::

  $ sudo apt-get install -y wget

Python 2.7 installieren::

  $ sudo apt-get install -y libxslt1-dev libxml2-dev
  $ sudo apt-get install -y python-dev python-imaging python-lxml

Setuptools installieren::

  $ wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py -O - | sudo python2.7

.. note::

  Distribute war ein Fork von Setuptools und lange Zeit die bevorzugte Variante zur Installation von Buildout. Mittlerweile ist Setuptools wieder die bessere Option.


Buildout
==============================================================================

Plone Verzeichnis erstellen::

  $ mkdir uebung-01

Download bootstrap Datei::

  $ cd uebung-01
  $ wget https://bootstrap.pypa.io/bootstrap-buildout.py

Datei "buildout.cfg" erstellen::

  [buildout]
  parts = instance
  extends = http://dist.plone.org/release/4.3.4/versions.cfg

  [instance]
  recipe = plone.recipe.zope2instance
  http-address = 8080
  user = admin:admin
  eggs = Plone

Buildout ausführen::

  $ python bootstrap-buildout.py
  $ bin/buildout

Zope Instanz starten (im "Foreground"-Modus)::

  $ bin/instance fg

Zope Instanz starten::

  $ bin/instance start

Zope Instanz stoppen::

  $ bin/instance stop


Versionskonflikte beheben
-------------------------

Mögliche Versionskonflikte (bei Ubuntu)::

  While:
    Installing.
    Getting section instance.
    Initializing section instance.
    Installing recipe plone.recipe.zope2instance.
  Error: There is a version conflict.
  We already have: zope.interface 4.0.5

.. note::
  Grund: Ubuntu verwendet eine alte Version von zope.interface.

Lösung: Version von zope.interface pinnen (buildout.cfg)::

  [versions]
  zope.interface = 4.0.5

Mögliche Probleme mit der verwendeten Buildout Version (buildout.cfg)::

  [versions]
  zc.buildout = 2.3.1

Output::

  The constraint, 0.6c11, is not consistent with the requirement, 'setuptools>=8.0'.
  While:
    Installing.
    Checking for upgrades.
  Error: Bad constraint 0.6c11 setuptools>=8.0

Lösung: Setuptools pinnen::

  [version]
  setuptools = 8.0.4

.. note::

  Liste von möglichen Buildout-Konflikten gibt es hier http://docs.plone.org/manage/troubleshooting/buildout.html

Bei Problemen: Löschen aller Buildout-Dateien::

  $ rm -rf bin develop-eggs/ parts/ .installed.cfg .mr.developer.cfg


Stabile Buildouts mit Version pinning
-------------------------------------

Vermeidung von Problemen in der Zukunft durch pinnen aller Versionen. Dies geht entweder über die Verwendung der Erweiterung "buildout.dumppickedversions" oder der Verwendung von zc.buildout > 2.1.0.

buildout.cfg::

  [buildout]
  extends = http://dist.plone.org/release/4.3.4/versions.cfg
  parts = instance
  show-picked-versions = true

Buildout erneut ausführen::

  $ bin/buildout

Versions pins in buildout.cfg kopieren (buildout.cfg):

  [versions]
  Products.PloneFormGen = 1.7.16
  Products.PythonField = 1.1.3
  Products.TALESField = 1.1.3
  Products.TemplateFields = 1.2.5

Buildout mit z3c.checkversions auf Aktualisierungen prüfen::

  [instance]
  recipe = plone.recipe.zope2instance
  ...
  eggs =
      ...
      z3c.checkversions

Fertiges buildout.cfg mit allen Erweiterungen:

.. literalinclude:: ../../uebung-01/buildout.cfg
