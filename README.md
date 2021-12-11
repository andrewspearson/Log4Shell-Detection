# Log4Shell Detection Cheat Sheet
## Tenable blog
**READ THIS FIRST**

https://www.tenable.com/blog/cve-2021-44228-proof-of-concept-for-critical-apache-log4j-remote-code-execution-vulnerability

## Identify Log4j installs without running a new scan
### Nessus Pro
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/np-log4j-installed.png)
### Tenable.io
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/tio-log4j-installed.png)

## Log4Shell plugins
https://www.tenable.com/plugins/search?q=cves%3A%28%22CVE-2021-44228%22%29&sort=&page=1
1. 155998 - Apache Log4j Message Lookup Substitution RCE (Log4Shell) (Direct Check)
**See note regarding this plugin below**
3. 155999 - Apache Log4j < 2.15.0 Remote Code Execution
4. 156000 - Apache Log4j Installed (Unix)
5. 156001 -  Apache Log4j JAR Detection (Windows)
6. 156002 - Apache Log4j < 2.15.0 Remote Code Execution

All plugins except for 155998 are also agent capable.

**These plugins are released in feed version 202112110647 and later. You might need to [force a plugin update](https://docs.tenable.com/nessus/Content/UpdateNessusSoftware.htm).**

**NOTE:**
Nessus plugin 155998 "Apache Log4j Message Lookup Substitution RCE (Log4Shell) (Direct Check)" will listen on a socket, perform a GET request with a JNDI:LDAP connection string in a few popular HTTP headers, and then wait for a LDAP connection back from the target. If the target connects back and we confirm it's trying to do a LDAP BIND, it will flag the target as vulnerable and output the proof.

Since this plugins listens for an LDAP BIND connect back it will not work on Tenable.io cloud scanners or in certain networks due to firewall rules. This plugin WILL work on Nessus Pro, Tenable.io linked scanners, and/or Tenable.sc linked scanners assuming a firewall does not block the connect back traffic.

A successful direct check finding will look like this:
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/direct-check-finding.png)

## Log4Shell scan template
A Log4Shell scan template has been released. This scan template contains all of the required scan settings to identify Log4Shell vulnerabilities.
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/log4shell-template.png)

## Log4Shell dashboards
### Tenable.io
https://www.tenable.com/tenable-io-dashboards/log4shell-critical-vulnerability
### Tenable.sc
https://www.tenable.com/sc-dashboards/log4shell-critical-vulnerability
