==============================================================================
Übung 6: Nützliche Erweiterungen für den Produktionsbetrieb
==============================================================================

Mailinglogger
-------------

deployment.cfg::

  [instance]
  eggs += mailinglogger
  mailinglogger =
    <mailing-logger>
      level error
      smtp-server localhost
      from server@company.com
      to me@company.com
      subject [Mein Server] [%(hostname)s] %(levelname)s - %(line)s
    </mailing-logger>


Sentry
------

deployment.cfg::

  [instance]
  eggs =
      ...
      raven
  event-log-custom =
    %import raven.contrib.zope
    <logfile>
      path ${buildout:directory}/var/log/${:_buildout_section_name_}.log
      level INFO
    </logfile>
    <sentry>
      dsn https://78fa32707202463d96d2d39b3fe316e2:15132297476c32378c03b6f00b389800@sentry.interaktiv.de/2
      level ERROR
    </sentry>


LongRequestLogger
-----------------

deployment.cfg::

    [instance]
    ...
    eggs =
        ...
        Products.LongRequestLogger
    zope-conf-additional =
      <environment>
        LOG_SLOW_QUERIES true
        LONG_QUERY_TIME 0.5
        longrequestlogger_file ${buildout:directory}/var/log/${:_buildout_section_name_}-longrequest.log
        longrequestlogger_timeout 4
        longrequestlogger_interval 2
      </environment>


Monitoring
----------

(Nagios, Munin)


ZODB Packen
-----------

https://pypi.python.org/pypi/plone.recipe.zeoserver


Backup/Restore
--------------

https://pypi.python.org/pypi/collective.recipe.backup


Logrotate
---------

https://pypi.python.org/pypi/plone.recipe.zope2instance

deployment.cfg::

  [instance]
  recipe = plone.recipe.zope2instance
  ...
  event-log-max-size = 5 MB
  event-log-old-files = 7
  access-log-max-size = 20 MB
  access-log-old-files = 7


ZEO-Replication
---------------

https://pypi.python.org/pypi/zc.zrs
https://pypi.python.org/pypi/plone.recipe.zeoserver
