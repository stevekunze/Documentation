---
tags:
  - Virtualization
  - arch
  - QEMU
  - KVM
---
# Installation 

1. Check if CPU supports virtualization (must be activated in BIOS/UEFI)
```shell
sudo lscpu | grep Virtualization
```
2. Activate support for nested VMs
```bash 
sudo modprobe -r kvm_intel
```
```bash 
sudo modprobe kvm_intel nested=1
```
3. Test if nested VMs work 
```bash
cat /sys/module/kvm_intel/parameters/nested
```
Return value should be **Y** or **1**.
4. Install packages 
```bash
sudo pacman -S qemu virt-manager libvirt virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat ebtables libguestfs tuned
```
5. Start and enable libvirt deamon 
```bash
sudo systemctl enable --now libvirtd
```
6. varify libvirt deamon status 
```bash
sudo systemctl status libvirtd
```
7. allow non root users to manage 
```bash
sudo micro /etc/libvirt/libvirtd.conf
```
Uncomment these lines 
```bash 
unix_sock_group = "libvirt"
unix_sock_group = "libvirt"
```
8. add user to libvertgroup and restart the service 
```bash
sudo usermod -a -G libvirt username
sudo systemctl restart libvirtd
```

## Firewalld for Endeavour OS 

```bash 
sudo micro /etc/firewalld/zones/libvirt.xml
```

```xml 
<?xml version="1.0" encoding="utf-8"?>
<zone target="ACCEPT">
  <short>libvirt</short>

  <description>
    The default policy of "ACCEPT" allows all packets to/from
    interfaces in the zone to be forwarded, while the (*low priority*)
    reject rule blocks any traffic destined for the host, except those
    services explicitly listed (that list can be modified as required
    by the local admin). This zone is intended to be used only by
    libvirt virtual networks - libvirt will add the bridge devices for
    all new virtual networks to this zone by default.
  </description>

<rule priority='32767'>
  <reject/>
</rule>
<protocol value='icmp'/>
<protocol value='ipv6-icmp'/>
<service name='dhcp'/>
<service name='dhcpv6'/>
<service name='dns'/>
<service name='ssh'/>
<service name='tftp'/>
</zone>
```

```bash 
sudo systemctl restart firewalld
```
## Tuned 

1. Enable TuneD daemon

```shell
sudo systemctl enable --now tuned.service
```

2. Check active TuneD profile

```shell
tuned-adm active
```

> Current active profile: balanced

- `balanced` - generic profile not specialised for KVM, we will change this.

3. List all TuneD profiles

```shell
tuned-adm list
```

4. Set profile to `virtual-host`

```shell
sudo tuned-adm profile virtual-host
```

5. Verify that TuneD profile

```shell
tuned-adm active
```

> Current active profile: virtual-host

```shell
sudo tuned-adm verify
```

