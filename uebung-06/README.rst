==============================================================================
Übung 6:
==============================================================================

Mailinglogger
-------------

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

Backup
------

(collective.recipe.backup, cronjob, restore)


Logrotate
---------

event-log-max-size = 5 MB
event-log-old-files = 7
access-log-max-size = 20 MB
access-log-old-files = 7

Supervisor
----------

ZEO-Replication
---------------

plone.app.caching
-----------------
