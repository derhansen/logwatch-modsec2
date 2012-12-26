Logwatch configuration for mod_security2 audit logfiles
=

What does it do?
-

This is a logwatch filter for mod_security2 audit logfiles. It collects events from
the audit log when an logentry contains:

* A hostname - e.g. www.site.tld
* An action - e.g. Intercepted (phase 2)

The filter creates a summary combined report for each virtual host and the attacks blocked.
It also displays the top 10 blocked IP addresses in the summary report.

It can help you analyzing your ModSecurity 2 audit logs to find blocked attacks or to find
false/positives.


Example output
-

 --------------------- ModSecurity2 (mod_security2) Begin ------------------------

 ATTACKS BLOCKED ON VHOSTS:

 subdomain.domain.tld - 2 time(s)
 [ip: xxx.xxx.xxx.xxx] [id: 981231 ] [msg: SQL Comment Sequence Detected.]  - 1 time(s)
 [ip: xxx.xxx.xxx.xxx] [id: 981231 ] [msg: SQL Comment Sequence Detected.]  - 1 time(s)

 www.site.tld - 1 time(s)
 [ip: xxx.xxx.xxx.xxx] [id: 990012 ] [msg: Rogue web site crawler]  - 1 time(s)
 [ip: xxx.xxx.xxx.xx] [id: 981318 ] [msg: SQL Injection Attack: Common Injection Testing Detected]  - 5 time(s)
 [ip: xxx.xxx.xxx.xx] [id: 950901 ] [msg: SQL Injection Attack: SQL Tautology Detected.]  - 2 time(s)

 www.anothersite.tld - 1 time(s)
 [ip: xxx.xxx.xxx.xxx] [id: 958291 ] [msg: Range: field exists and begins with 0.]  - 1 time(s)

 TOP 10 BLOCKED IPS:

 xxx.xxx.xxx.xxx - 2 time(s)
 xx.xxx.xxx.xxx - 1 time(s)
 xxx.xxx.xx.xx - 1 time(s)
 xxx.xxx.xxx.xx - 1 time(s)
 xxx.xxx.xxx.xxx - 1 time(s)

 ---------------------- ModSecurity2 (mod_security2) End -------------------------


Compatibility
-

The filter has been tested with ModSecurity 2 version 2.7.1 and the OWASP ModSecurity Core Rule Set (CRS)


Installation
-

1. Copy 'conf/logfiles/audit_log.conf' to '/etc/logwatch/conf/logfiles'
2. Copy 'conf/services/mod_security2.conf' to '/etc/logwatch/conf/services'
3. Copy 'scripts/services/mod_security2' to '/etc/logwatch/scripts/services'

Adjust the settigns for the logfile to match the location of your mod_security2 logfiles.


Usage
-

Display logfile entries (default output)

~# logwatch --service mod_security2

Display logfile entries for a given date (or date range)

~# logwatch --service mod_security2  --range 10/Dec/2012


Feedback / Improvements
-

Feel free to provide feedback or suggestions for improvement.