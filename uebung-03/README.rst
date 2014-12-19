==============================================================================
Übung 3: Entwicklung mit Buildout
==============================================================================

Plone Pakete mit mr.developer verwalten
---------------------------------------

Installation von mr.developer (buildout.cfg)::

  [buildout]
  extends = http://dist.plone.org/release/4.3.4/versions.cfg
  parts = instance
  extensions = mr.developer
  auto-checkout = Products.PloneFormGen

  ...
  [sources]
  Products.PloneFormGen = git git://github.com/collective/Products.PloneFormGen.git

Lokale Pakete verwalten::

  [sources]
  my.policy = fs my.policy
  my.contenttypes = fs my.contenttypes
  my.theme = fs my.theme


Products.PDBDebugMode
---------------------

PDB Debugger wird automatisch in der Konsole gestartet wenn ein Fehler auftritt::

  (Pdb) pp request


Products.PrintingMailHost
-------------------------

Loggt versendete Mails in der Konsole.

Mail-Einstellungen im Mail Control Panel einstellen und Testmail versenden::

  2014-12-19 09:18:47 INFO Zope Ready to handle requests

  ---- sending mail ----
  From: foo@bar.com
  To: ['foo@bar.com']
  From nobody Fri Dec 19 09:19:36 2014
  MIME-Version: 1.0
  Content-Type: text/plain; charset="utf-8"
  Content-Transfer-Encoding: quoted-printable
  Subject: =?utf-8?q?Test_e-mail_from_Plone?=
  To: foo@bar.com
  From: foo@bar.com
  Date: Fri, 19 Dec 2014 09:19:36 +0100

  Hi,

  This is a test message sent from the Plone 'Mail settings' control panel. Y=
  our receipt of this message (at the address specified in the Site 'From' ad=
  dress field) indicates that your e-mail server is working!

  Have a nice day.

  Love,

  Plone
  ---- done ----


plone.app.debugtoolbar
----------------------

.. image:: _images/plone.app.debugtoolbar.png


plone.reload
------------

Startet Plone nach Code-Änderungen automatisch neu.


collective.backtowork
---------------------

Zeigt an wenn die Plone Instanz wieder erreichbar ist (Ubuntu).


Buildout
--------

Fertiges buildout.cfg:

.. literalinclude:: ../../uebung-03/buildout.cfg
