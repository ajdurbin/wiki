### Installation 
  - Choose 64-bit memstick version
  - username admin, hardware password
  - hostname: `erie`, domain: `localdomain`
  - Add `OPT1, OPT2` interfaces and copy firewall rules 
  - Copy `LAN` interface configuration to `OPT` interfaces
  - Change DNS servers to Google, OpenDNS
  - Change DHCP server available range
  - Do not allow DNS server list to be overridden

### PFBlockerNG 
  - `Firewall -> PFBlockerNG`
  - Control/Command click all outbound firewall rules except for lan and save
  - Go to `DNSBL`
  - Add new `DNSBL` feeds, add DNS group name, eg pi-hole, description uses default pi-hole lists, add each pi-hole list to `DNSBL` and add 'test' for header/description
  - List actio switched to unbound and update every hour 
  - Save, update, force update and watch lists download
  - Enable and save
  - Do same with EasyList `DNSBL`, check all, label as test and force update again

### Use hostnames for SSH 
From `https://www.bytesizedalex.com/pfsense-dns-resolution-for-dhcp-leases/`. Go to DNS Resolver and check Register DHCP leases and Register DHCP static mappings.