# SCO OpenServer 6 on KVM

Progress so far: up-to-date SCO OpenServer 6 installed and running, timekeeping is working.

#### System
 - Fedora 32, 64-bit
 - Linux 5.9.0-rc3

#### Issues to fix
 - None

#### Installation process
 - Create the VM
    - Set the hard drive to SATA (AHCI), and the CDROM to SCSI
    - Set CPU type to `pentium`
    - Edit the XML (via `virsh edit <name>` or the XML tab in `virt-manager`) and remove the line `<acpi/>`
 - Use the [boot][boot] iso to boot the VM
 - When prompted, insert the [main][mainiso] installation image
 - When the install is finished, **DO NOT REBOOT**
 - Insert [MP4][mp4] image
 - Use the software manager to install the MP4 updates
 - Insert [OSS711][oss711] image
 - Use the software manager to install the OSS711e updates
 - Reboot
 - Edit `/stand/boot` and add a line saying `ACPI=Y`
 - Reboot
 
 
#### Random  notes
 - [nd.806n][nd] latest network driver as of Sep 2020
 - Make sure the CDROM device has the address of 0:0:0 on the SCSI bus
 - The ACPI stuff above has to do with timekeeping. I have no idea why it requires those steps for timekeeping to work, but it does. Disabling ACPI in KVM, and telling SCO to use ACPI. *WHY* does that work? If anyone has an idea please tell me!!
  - (Maybe there's a fallback timekeeping method that's only triggered when ACPI use is attempted and fails?)

<hr />

##### Source(s):
 - [Installation issues while installing OpenServer 6][instissues] - SCO Sales
 - [Revisiting a UnixWare 7.1.1 install on Qemu/KVM][revisit] - Virtually Fun
  - [And it’s live now - SCO Open Server 5.0.5 running in a RHEL 6 KVM][livenow] - Harish Pillay

[livenow]: https://harishpillay.com/2012/05/08/and-its-live-now-sco-open-server-5-0-5-running-in-a-rhel-6-kvm/
[boot]: ftp://ftpput.sco.com/tmp/support/ISO/OpenServer-6.0.0Ni-boot-2012-12-04.iso
[nd]: ftp://ftp.sco.com/pub/openserver6/600/drivers/nd.806n/nd.806n.image
[mainiso]: ftp://ftp.sco.com/pub/openserver6/600/iso/OpenServer-6.0.0-Mar2006/OpenServer-6.0.0Ni-2006-02-08-1513.iso
[mp4]: ftp://ftp.sco.com/pub/openserver6/600/mp/osr600mp4/osr600mp4_cd1.iso
[oss711]: ftp://ftp.sco.com/pub/openserver6/600/patches/oss711e/oss711e.iso
[instissues]: https://www.scosales.com/ta/kb/127884.html
[revisit]: https://virtuallyfun.com/wordpress/2018/01/31/revisiting-a-unixware-7-1-1-install-on-qemu-kvm/