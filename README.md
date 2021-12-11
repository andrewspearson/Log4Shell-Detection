# Log4Shell-Detection
## Change Log
1. 20211211u1: Creation

## Tenable blog
https://www.tenable.com/blog/cve-2021-44228-proof-of-concept-for-critical-apache-log4j-remote-code-execution-vulnerability

## Identify Log4j installs without running a new scan
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/search.png)

## Log4Shell plugins
1. 155998 - Apache Log4j Message Lookup Substitution RCE (Log4Shell) (Direct Check)
**See note regarding this plugin below**
3. 155999 - Apache Log4j < 2.15.0 Remote Code Execution
4. 156000 - Apache Log4j Installed (Unix)
5. 156001 -  Apache Log4j JAR Detection (Windows)
6. 156002 - Apache Log4j < 2.15.0 Remote Code Execution

These plugins are released in feed version **202112110647** and later. You might need to [force a plugin update](https://docs.tenable.com/nessus/Content/UpdateNessusSoftware.htm).

**NOTE:**
Nessus plugin 155998 "Apache Log4j Message Lookup Substitution RCE (Log4Shell) (Direct Check)" will listen on a socket, perform a GET request with a JNDI:LDAP connection string in a few popular HTTP headers, and then wait for a LDAP connection back from the target. If the target connects back and we confirm it's trying to do a LDAP BIND, it will flag the target as vulnerable and output the proof.

Since this plugins listens for an LDAP BIND connect back it will not work on Tenable.io cloud scanners or in certain networks due to firewall rules.

A successful direct check finding will look like this:
![](https://github.com/andrewspearson/file-server/blob/main/repositories/log4shell-detection/direct-check-finding.png)

## Log4Shell scan template
