==============================================================================
Übung 4: Deployment mit Buildout
==============================================================================

Entwicklungs-Buildout (buildout.cfg):

.. literalinclude:: ../../uebung-04/buildout.cfg

Deployment-Buildout (deployment.cfg):

.. literalinclude:: ../../uebung-04/deployment.cfg

Deployment Buildout ausführen::

  $ python bootstrap-buildout.py -c deployment.cfg
  $ bin/buildout -c deployment.cfg

Deployment Instanz starten::

  $ bin/instance fg
  2014-12-19 09:30:26 INFO ZServer HTTP server started at Fri Dec 19 09:30:26 2014
    Hostname: 0.0.0.0
    Port: 9999
  ...
