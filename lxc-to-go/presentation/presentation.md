# LXC-to-Go
## (rapid lxc deployment for mobile devices and servers)

- Daniel ([github](https://github.com/plitc))
- Slides & Code: [github.com/plitc/lxc-to-go](https://github.com/plitc/lxc-to-go)



## Ablauf

1. Konzept / Motivation
2. Features
3. Grundlagen
4. Demo

Note:
- Grundlagen:



## Konzept / Motivation

- einfache Container Lösung!
 * fertige LXC configs & templates
 * auch geeignet für Laptops mit wechselnder Netzanbindung
- erstellt Managed Container für DHCP, DNS & RA Services
- automatische NAT Portforwarding Regeln für interne LXCs
 * IPv4 192.168.254.xxx/24
 * IPv6 fd00:xxxx/64
- PulseAudio Control der internen LXCs
- Graphics Acceleration in internen LXCs
- Nested LXC / LXC-inside-LXC Container Webpanel
 * für Wegwerf inside LXC, Docker Container



## Schema

<a href="content/lxc-to-go_schema_.jpg">
   <img src="content/lxc-to-go_schema_.jpg" height="600">
</a>



## Bootstrap

```shell
╭─root at it-daniel in ~ using
╰─○ lxc-to-go bootstrap

[  OK  ] 'optional: fixes for lmde'
WARNING: disable AppArmor on Debian & Ubuntu!
[  OK  ] 'optional: fixes for ubuntu'
[  OK  ] 'optional: fixes for devuan'
[  OK  ] 'optional: debian wheezy upgrade information'
[  OK  ] 'create lxc-to-go directory'
[  OK  ] 'create lxc-to-go/tmp directory'
[  OK  ] 'copy hook_provisioning.sh'
[  OK  ] 'copy template.func.sh'
[  OK  ] 'lxc-to-go environment configcheck'
[  OK  ] 'lxc-to-go interface configcheck'
[  OK  ] 'lxc-to-go btrfs configcheck'
[  OK  ] 'look over cgmanager'
Synchronizing state of cgmanager.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable cgmanager
[  OK  ] 'look over cgmanager'
[  OK  ] 'look over screen'
[  OK  ] 'look over iptables'
[  OK  ] 'look over ip6tables'
[  OK  ] 'look over lxc'
[  OK  ] 'look over debootstrap'
[  OK  ] 'lxc template - wheezy configcheck'
[  OK  ] 'look over bridge-utils'
[  OK  ] 'look over net-tools'
Kernel configuration not found at /proc/config.gz; searching...
Kernel configuration found at /boot/config-4.16.0-2-amd64
--- Namespaces ---
Namespaces: enabled
Utsname namespace: enabled
Ipc namespace: enabled
Pid namespace: enabled
User namespace: enabled
Network namespace: enabled

--- Control groups ---
Cgroups: enabled

Cgroup v1 mount points:
/sys/fs/cgroup/systemd
/sys/fs/cgroup/net_cls,net_prio
/sys/fs/cgroup/blkio
/sys/fs/cgroup/devices
/sys/fs/cgroup/memory
/sys/fs/cgroup/pids
/sys/fs/cgroup/cpu,cpuacct
/sys/fs/cgroup/perf_event
/sys/fs/cgroup/cpuset
/sys/fs/cgroup/freezer

Cgroup v2 mount points:
/sys/fs/cgroup/unified

Cgroup v1 clone_children flag: enabled
Cgroup device: enabled
Cgroup sched: enabled
Cgroup cpu account: enabled
Cgroup memory controller: enabled
Cgroup cpuset: enabled

--- Misc ---
Veth pair device: enabled, loaded
Macvlan: enabled, not loaded
Vlan: enabled, not loaded
Bridges: enabled, loaded
Advanced netfilter: enabled, not loaded
CONFIG_NF_NAT_IPV4: enabled, loaded
CONFIG_NF_NAT_IPV6: enabled, loaded
CONFIG_IP_NF_TARGET_MASQUERADE: enabled, loaded
CONFIG_IP6_NF_TARGET_MASQUERADE: enabled, loaded
CONFIG_NETFILTER_XT_TARGET_CHECKSUM: enabled, not loadedCONFIG_NETFILTER_XT_MATCH_COMMENT: enabled, not loaded
FUSE (for use with lxcfs): enabled, loaded

--- Checkpoint/Restore ---
checkpoint restore: enabled
CONFIG_FHANDLE: enabled
CONFIG_EVENTFD: enabled
CONFIG_EPOLL: enabled
CONFIG_UNIX_DIAG: enabled
CONFIG_INET_DIAG: enabled
CONFIG_PACKET_DIAG: enabled
CONFIG_NETLINK_DIAG: enabled
File capabilities: enabled

Note : Before booting a new kernel, you can check its configuration
usage : CONFIG=/path/to/config /usr/bin/lxc-checkconfig

[  OK  ] 'optional: wheezy kernel upgrade'
[  OK  ] 'optional: wheezy lxc upgrade'
[  OK  ] 'grub configcheck'
[  OK  ] 'optional: powerpc / travis-ci environment configcheck'
[  OK  ] 'modprobe: iptables/nf_nat'
[  OK  ] 'prepare bridge zones - stage 1'
[  OK  ] 'prepare bridge zones - stage 2'
[  OK  ] 'prepare bridge zones - stage 3'
[  OK  ] 'lxc: managed bootstrap - stage 1'
[  OK  ] 'lxc: managed bootstrap - stage 2'
[  OK  ] 'configure host sysctl'
[  OK  ] 'optional: fixes for ubuntu'
[  OK  ] 'lxc: deb7template'
... LXC Container (screen session: ): always running ...
[  OK  ] 'lxc: managed bootstrap - stage 3'
[  OK  ] 'lxc: managed upgrade - stage 1'
[  OK  ] 'lxc: managed upgrade - stage 2'
[  OK  ] 'lxc: managed look over iptables'
[  OK  ] 'lxc: managed sysctl'
[  OK  ] 'lxc: managed rc.local'
[  OK  ] 'lxc: managed network settings'
[  OK  ] 'lxc: managed look over less'
[  OK  ] 'lxc: managed look over isc-dhcp-server'
[  OK  ] 'lxc: managed isc-dhcp-server configcheck'
[  OK  ] 'lxc: managed look over unbound'
[  OK  ] 'lxc: managed unbound configcheck'
[  OK  ] 'lxc: managed look over radvd'
[  OK  ] 'lxc: managed radvd configcheck'
[  OK  ] 'lxc: managed look over iputils-ping'
[  OK  ] 'lxc: managed look over traceroute'
[  OK  ] 'lxc: managed look over dnsutils'
[  OK  ] 'lxc: managed look over mtr-tiny'
[  OK  ] 'prepare bridge zones - stage 4'
[  OK  ] 'prepare bridge zones - stage 5'
[  OK  ] 'configure rp_filter sysctl'
[  OK  ] 'configure lxc-to-go symlinks - stage 1'
[  OK  ] 'configure lxc-to-go symlinks - stage 2'
[  OK  ] 'configure lxc-to-go etc/hosts entry'
Verbindungsfehler: Verbindung verweigert
pa_context_new() fehlgeschlagen: Verbindung verweigert
[FAILED] 'PulseAudio Access denied! but skipping ...'
[ INFO ] PulseAudio maybe listen on (vswitch0) Port 4713 now!
[  OK  ] 'optional: prepare lxc x11 video / audio environment'

● isc-dhcp-server.service - LSB: DHCP server
   Loaded: loaded (/etc/init.d/isc-dhcp-server)
   Active: active (running) since Mi 2018-09-19 09:26:31 CEST; 2 days ago
  Process: 161 ExecStart=/etc/init.d/isc-dhcp-server start (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/isc-dhcp-server.service
           └─169 /usr/sbin/dhcpd -q -cf /etc/dhcp/dhcpd.conf -pf /var/run/dhcpd.pid

Hint: Some lines were ellipsized, use -l to show in full.
[  OK  ] 'lxc: managed isc-dhcp-server'

● unbound.service - (null)
   Loaded: loaded (/etc/init.d/unbound)
  Drop-In: /run/systemd/generator/unbound.service.d
           └─50-insserv.conf-$named.conf, 50-unbound-$named.conf
   Active: active (running) since Mi 2018-09-19 09:26:29 CEST; 2 days ago
  Process: 109 ExecStart=/etc/init.d/unbound start (code=exited, status=0/SUCCESS)
 Main PID: 159 (unbound)
   CGroup: /system.slice/unbound.service
           └─159 /usr/sbin/unbound

Hint: Some lines were ellipsized, use -l to show in full.
[  OK  ] 'lxc: managed unbound'

● radvd.service - LSB: Router Advertising Daemon
   Loaded: loaded (/etc/init.d/radvd)
   Active: active (running) since Mi 2018-09-19 09:26:27 CEST; 2 days ago
  Process: 107 ExecStart=/etc/init.d/radvd start (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/radvd.service
           ├─129 /usr/sbin/radvd -u radvd -p /var/run/radvd/radvd.pid
           └─131 /usr/sbin/radvd -u radvd -p /var/run/radvd/radvd.pid

[  OK  ] 'lxc: managed radvd'
[  OK  ] 'optional: sysctl for unprivileged containers'
[  OK  ] 'optional: load fuse module for unprivileged containers'
fs.file-max = 99000000
[  OK  ] 'optional: file-max support up to 99 lxc'
[  OK  ] 'clean up tmp files'

lxc-to-go bootstrap finished.
╭─root at it-daniel in ~ using
╰─○
```



## Motivation

- Automatisierung
- Statistiken/Langzeitdaten
- Andere Darstellung/Mashups



## Grundlagen

- Was brauchen wir:
  - eine Programmiersprache,  ✓ ([Python](python.org))
  - die Webseiten herunterladen kann ✓ ([Requests](http://docs.python-requests.org/en/latest/))
  - und parsen kann ✓ ([BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/))

Note:
- Viele Programmiersprachen sind grundsätzlich geeignet.
- Ich bevorzuge dynamische Programmiersprachen, wegen interaktiven Shell (später
  mehr)
- Wir müssten wie der Browser HTTP sprechen, Python kann das von Haus aus.
  Requests ist aber schöner zu benutzen
- Letztendlich muss das HTML der Webseite ausgewertet werden



## Grundlagen - HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Präsidenten</title>
  </head>
  <body>
    <table id="präsidenten">
      <tr>
        <th>Präsidenten</th>
        <th>Regierungszeiten</th>
      </tr>
      <tr>
        <td>Abraham Lincoln</td>
        <td class="date">4. März 1861 - 15. April 1865</td>
      </tr>
      <tr>
        <td>Andrew Johnson</td>
        <td class="date">15. April 1865 - 4. März 1869</td>
      </tr>
      <tr>
        <td>Ulysses S. Grant</td>
        <td class="date">4. März 1869 - 4. März 1877</td>
      </tr>
    </table>
  </body>
</html>
```



## Grundlagen - CSS Selektoren

<table>
<tr><td>Selector</td> <td>Example</td> <td>Example description CSS</td></tr>
<tr><td>.class</td> <td>.date</td> <td>Wählte alle Zeilen mit der Klasse .date aus.</td></tr>
<tr><td>#id</td> <td>#präsidenten</td> <td>Wählt die Tabelle mit der ID Präsident aus.</td></tr>
<tr><td>element</td> <td>tr</td> <td>Wählt alle Zeilen der Tabelle aus.</td></tr>
<tr><td>Komplexbeispiel</td> <td>#präsidenten tr:first-child</td> <td>1. Zeile der Präsidententabelle</td></tr>
</table>




## Grundlagen - CSS Selektoren
- Einführung für [CSS-Selektoren](https://developer.mozilla.org/de/docs/Web/Guide/CSS/Getting_started/Selektoren)
- Einführung für [XPath](https://de.wikipedia.org/wiki/XPath)



## Grundlagen - Beispiel

```python
#!/usr/bin/env python
import requests, random
from bs4 import BeautifulSoup

url = "https://en.wikipedia.org/wiki/Nicolas_Cage_filmography"
doc = requests.get(url)
soup = BeautifulSoup(doc.text, 'html.parser')
rows = soup.select("table.wikitable.sortable tr")
choice = random.choice(rows)
print(choice.select("td i a")[0].text)
```

```bash
$ python3 random_cage.py
```



## Beispiel

Luzern: http://www.pls-luzern.ch/de



## Ihr seid dran

- Vorschlag:
  - Bregenz: https://www.bregenz.gv.at/sicherheit-verkehr/verkehr-und-parken/parkleitsystem.html
  - [Andere Beispiele](https://github.com/offenesdresden/ParkAPI/issues?q=is%3Aclosed+label%3Anew_data+is%3Aissue)
- Python Referenz: http://www.cs.put.poznan.pl/csobaniec/software/python/py-qrc.html
- Beautiful Soup: http://www.crummy.com/software/BeautifulSoup/bs4/doc/
- Requests: http://docs.python-requests.org/en/latest/
