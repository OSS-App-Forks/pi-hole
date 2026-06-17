# Static DHCP Hostname Resolution

Restored support for tracking and resolving static DHCP hostnames separately from active leases. This ensures that devices with static IP configurations in Pi-hole's DHCP server can always be resolved by name, even if they have not recently requested a lease.

## Changes
- **New CLI Commands**:
  - `pihole adddhcphostname <mac> <ip> <hostname>`: Adds a static entry to `/etc/pihole/hosts/static-dhcp.list`.
  - `pihole removedhcphostname <mac>`: Removes a static entry based on its MAC address.
- **Automatic Configuration**:
  - Automatically creates `/etc/dnsmasq.d/99-pihole-static-dhcp.conf` to include the static hosts file via the `addn-hosts` directive.
  - Automatically fetches the configured DNS domain (`dns.domain.name`) and creates consolidated records (`IP FQDN Hostname`) for complete resolution support.
- **Service Integration**:
  - Automatically reloads the DNS service after changes to apply new records immediately.
