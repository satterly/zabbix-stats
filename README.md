Zabbix Server Statistics
========================

Get access to internal zabbix server performance statistics
for reporting and graphing using tools like Ganglia, Cacti etc.

### Statistics ###

The following statistics are available:

<pre>
 | STATISTIC         | SOURCE OF VALUE                    | 
 +-------------------+------------------------------------+
 | version, revision | ZABBIX_VERSION, ZABBIX_REVISION    |
 | boottime          | zabbix["boottime"]                 | 
 | uptime            | zabbix["uptime"]                   |
 | time              | time()                             |
 | items_total       | zabbix["items"]                    |
 | items_unsupported | zabbix["items_unsupported"]        |
 | triggers_total    | zabbix["triggers"]                 |
 | items_queue       | zabbix["queue",0,-1]               |
 | required_perf     | zabbix["requiredperformance"]      |
 | wcache_total      | zabbix["wcache", "values", "all"]  |
 | rcache_free       | zabbix["rcache", "buffer", "free"] | 
 | threads           | threads_num                        | 
</pre>

### Usage ###

Telnet to port 10051 on the Zabbix server and type "stats". All available
stats will be returned, one per line, prepended with STAT and then 
terminated with an END.

### Example ###

<pre>
# telnet localhost 10051
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
stats
STAT version 1.8.5 rev 19050
STAT boottime 1308513407
STAT uptime 29
STAT time 1308513436
STAT items_total 5089
STAT items_unsupported 9
STAT triggers_total 1050
STAT items_queue 2
STAT required_perf 2.03
STAT wcache_total 58
STAT rcache_free 8279480
STAT threads 26
END
</pre>

### Modifications ###

Only three files have been modified...

* src/zabbix_server/poller/checks_internal.c
* src/zabbix_server/poller/checks_internal.h
* src/zabbix_server/trapper/trapper.c

### Install Instructions ###

1. `./configure --enable-server --with-mysql`
2. `make`
3. `make install`

### Original Source Code ###

The original source code is available on [SourceForge](http://sourceforge.net/projects/zabbix/).
