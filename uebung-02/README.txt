==============================================================================
Übung 2: Installation von Erweiterungen für Plone
==============================================================================

Erweiterungen finden
==============================================================================

- http://plone.org/products
- http://pypi.python.org/pypi
  - plone.*
  - plone.app.*
  - collective.*
  - Products.*


Erweiterung Installieren
==============================================================================

buildout.cfg::

  [instance]
  eggs =
    Plone
    Products.PloneFormGen
    plone.app.contenttypes

Buildout nochmals laufen lassen::

  $ bin/buildout

Instanz starten::

  $ bin/instance fg
