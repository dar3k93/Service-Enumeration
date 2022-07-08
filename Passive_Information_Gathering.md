# Passive Information Gathering
also known as Open-source Intelligence or OSINT. Is the process of collecting openly available information about a target, generally without any direct interaction
with that target.

## Website Recon

- Whois Enumeration
Is a TCP service, tool, and a type of database that can provide information about a domain name, such as the name server140 and registrar.
```
> whois my_osint.eu
```
forward lookup, which gathers information about a DNS name, the whois client can also perform reverse lookups. Assuming we have an IP address, we can perform
a reverse lookup to gather more information about it:
```
> whois 10.200.10.1
```

## Google Hacking
!!!!!!!!!!!!!Google Hacking for Penetration Testers!!!!!!!!!!!!!!

## Netcraft
Is an Internet services company offering a free web portal that performs various information gathering functions. 

- Netcraft DNS search:
```
https.//searchdns.netcraft.com
```

## Recon-ng
is a module-based framework for web-based information gathering
```
> recon-ng
```
We need to install various modules to use recon-ng. We can add modules from the recon-ng "Marketplace".
```
> marketplace search
[...]
> marketplace search github
```
We can learn more about a module by using marketplace info
```
> marketplace info recon/domains-hosts/google_site_web
```
We can install module by using install parameter
```
> marketplace install recon/domains-hosts/google_site_web
```
After installing the module, we can load it with module load followed by its name
```
modules load recon/domains-hosts/google_site_web
```
We will use options set SOURCE my_osint.eu to set our target domain
```
options set SOURCE my_osint.eu
[...]
run
```
## Open-Source Code

## Shodan


