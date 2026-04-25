# Overwatch Enrollment

AtomicNix is moving toward an Overwatch-managed enrollment and remote-access model.

## Bootstrap Flow

1. The device boots with no embedded remote-management credential.
2. The Overwatch client identifies the device using the `eth0` MAC address.
3. Overwatch checks that MAC against an approved inventory list.
4. If approved, Overwatch returns a registration key.
5. The device persists that registration key on `/data` for future authenticated requests.
6. Overwatch can then issue short-lived SSH credentials and establish remote sessions through the reverse tunnel managed
   by the device client.

## Trust Model

- The MAC address is an identifier, not a secret.
- Inventory approval determines whether a device is eligible to enroll.
- The registration key is the first durable management credential.
- Short-lived SSH credentials are issued dynamically by Overwatch and expire automatically.

## Device Responsibilities

AtomicNix remains responsible for:

- local LAN gateway services (`dnsmasq`, `chrony`, firewall)
- SSH access for LAN/VPN recovery
- RAUC update and rollback flow
- persistent storage of enrollment state on `/data`

Remote web management is intended to be hosted by Overwatch rather than directly by the device.
