# rosa-resolver-patch
The resolver is probably incorrectly configured in the ROSA Linux distribution.  
  
/etc/systemd/resolved.conf.patch
```
--- resolved.conf
+++ resolved.conf
@@ -20,8 +20,8 @@
 # Google:     8.8.8.8#dns.google 8.8.4.4#dns.google 2001:4860:4860::8888#dns.google 2001:4860:4860::8844#dns.google
 # Quad9:      9.9.9.9#dns.quad9.net 149.112.112.112#dns.quad9.net 2620:fe::fe#dns.quad9.net 2620:fe::9#dns.quad9.net
 #DNS=
-#FallbackDNS=77.88.8.8 77.88.8.1 8.8.8.8 8.8.4.4
-#Domains=
+FallbackDNS=9.9.9.9 149.112.112.112 2620:fe::fe 2620:fe::9
+Domains=~.
 #DNSSEC=no
 #DNSOverTLS=no
 #MulticastDNS=resolve
```
After the uninstall, the file `/etc/systemd/resolved.conf` are returned by default.  
  
**Note:** Additionally, the patch eliminates **DNS leaks**, since by default, ROSA `FallbackDNS` uses unreliable `Yandex` DNS servers. Patch allows you to use, for example, Cloudflare (TM) WARP (see [warpgui](https://github.com/AKotov-dev/warpgui)) or VPNs securely. Tested in ROSA-12.4-PLASMA/XFCE.
