---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# USBSTOR Key

The `USBSTOR` key is the primary, indestructible ledger of every USB mass-storage class device ever connected to the host system.

**Registry Path:** `HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR`

Keys under this directory are structured using hardware identifiers: `Disk&Ven_[Vendor]&Prod_[Product]&Rev_[Revision]\[DeviceSerialNumber]`

***

## Unique Serial Numbers

When analysing a device's serial number string within `USBSTOR`, look closely at the second character.

If the second character is an ampersand (`&`) (e.g. `7&2a8df9e&0`), the device does not possess a unique serial number written to its firmware by the manufacturer. Windows has programmatically generated a ParentIdPrefix to identify it. We cannot rely on this serial number to uniquely identify this specific physical stick across other suspect machines.

If there is no ampersand at the second character (e.g. `001D923F900B`), it is a globally unique, manufacturer-assigned serial number. This is your target identifier; you can use it to prove the exact same physical thumb drive was used across multiple victim workstations.

***

## Timestamps

Modern Windows systems (**Windows 8, 10, & 11**) record explicit, device-specific timestamps within the subkey's properties block:

* `0x64` (InstallDate): The timestamp when the device driver was most recently successfully installed.
* `0x65` (FirstInstallDate): The first time the device was introduced to the system.
* `0x66` (LastArrivalDate): The most recent time the physical USB was plugged in.
* `0x67` (LastRemovalDate): The most recent time the device was safely unmounted or disconnected.

These timestamps are stored in UTC FILETIME format, providing a highly reliable tracking window for the device's last active session.
