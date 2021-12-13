# Log4Shell Detection Cheat Sheet
## Tenable blog
**READ THIS FIRST**

https://www.tenable.com/blog/cve-2021-44228-proof-of-concept-for-critical-apache-log4j-remote-code-execution-vulnerability

## Identify Log4j installs without running a new scan
Organizations that have been running recurring scans can simply query for all log4j installs. This will provide an immediate list of hosts likely vulnerable to Log4Shell without having to wait for new scan results. This will of course require previous authenticated scans and the results will not be valid once remediation efforts have started.
### Nessus Pro
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/np-log4j-installed-v2.png)
### Tenable.io
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/tio-log4j-installed.png)

## Log4Shell plugins
Plugins are listed here:
https://www.tenable.com/plugins/search?q=cves%3A%28%22CVE-2021-44228%22%29&sort=&page=1

There are two remote uncredentialed Nessus plugins:

**1. 155998 - Apache Log4j Message Lookup Substitution RCE (Log4Shell) (Direct Check)**  
When this plugin is launched the scanner will listen on a random ephemeral port, perform a GET request with a connection string, and then wait for a connection back from the target to the random ephemeral port the scanner is listening on. If the target connects back trying to perform an LDAP BIND the plugin flags as vulnerable. Since this plugins listens for an LDAP BIND connect back it will not work on Tenable.io cloud scanners or in certain networks due to firewall rules. This plugin WILL work on Nessus Pro, Tenable.io linked scanners, and/or Tenable.sc linked scanners assuming a firewall does not block the connect back traffic. This plugin became available in feed version 202112110647 and later. Example:
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/155998-np.png)

**2. 156014 - Apache Log4Shell RCE detection via callback correlation (Direct Check HTTP)**  
This plugin does not require a connect back to the Nessus scanner and will work on Tenable.io cloud scanners. This plugin will make a DNS lookup to verify the presence of the vulnerability. This plugin became available in feed version 202112112213 and later. Example:
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/156014-np.png)

There are many local/authenticated plugins that are also agent capable.

There is also a remote uncredentialed WAS plugin that performs additional checks.

The Nessus plugins will identify Log4Shell vulns in areas that the WAS scanner will not and vice-versa. Organization need to run scans from Nessus/Tenable.io/Tenable.sc AND Tenable WAS in parallel, immediately.

## Log4Shell scan template
A Log4Shell scan templates have been released in Nessus, Tenable.io, Tenable.sc, and Tenable WAS. This scan template contains all of the required scan settings and plugins to identify Log4Shell vulnerabilities. For now, use this template to find Log4Shell and not a regular full vuln scan. The Log4Shell scan template runs extraordinarily fast.
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/log4shell-template.png)

## Log4Shell dashboards
### Tenable.io
https://www.tenable.com/tenable-io-dashboards/log4shell-critical-vulnerability
### Tenable.sc
https://www.tenable.com/sc-dashboards/log4shell-critical-vulnerability
