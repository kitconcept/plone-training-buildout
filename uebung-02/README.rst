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

Buildout nochmals laufen lassen::

  $ bin/buildout

Instanz starten::

  $ bin/instance fg


Stabile Buildouts mit Version pinning
-------------------------------------

Vermeidung von Problemen durch pinnen aller Versionen der verwendeten Add-on Produkte. Dies geht entweder über die Verwendung der Erweiterung "buildout.dumppickedversions" oder der Verwendung von zc.buildout > 2.1.0.

buildout.cfg::

  [buildout]
  extends = http://dist.plone.org/release/4.3.4/versions.cfg
  parts = instance
  show-picked-versions = true

Buildout erneut ausführen::

  $ bin/buildout

Versions pins in buildout.cfg kopieren (buildout.cfg)::

  [versions]
  Products.PloneFormGen = 1.7.16
  Products.PythonField = 1.1.3
  Products.TALESField = 1.1.3
  Products.TemplateFields = 1.2.5


Buildout auf Aktualisierungen prüfen
------------------------------------

Buildout mit z3c.checkversions auf Aktualisierungen prüfen::

  [instance]
  recipe = plone.recipe.zope2instance
  ...
  eggs =
      ...
      z3c.checkversions

Fertiges buildout.cfg mit allen Erweiterungen:

.. literalinclude:: ../../uebung-02/buildout.cfg
