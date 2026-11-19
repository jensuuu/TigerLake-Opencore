# OpenCore EFI for HP DW3018NO (Tiger Lake)

OpenCore EFI / `config.plist` for the HP DW3018NO laptop. Work in progress, so expect rough edges.

## Current Working Status

| Feature | Status |
| --- | --- |
| Boots into macOS Recovery (macrecovery) | ✅ Works |
| Ethernet | ✅ Works |
| WhateverXe (Xe iGPU) support | ✅ Added |
| Wi-Fi | ❌ Not working |
| Touchpad in the Recovery/installer screen | ❌ Not working |
| Intel RST/VMD disks | ❌ Not detected |

**Disk limitation:** only external USB disks or non-RST/VMD disks can be used.

## To Make It Work

1. Remove `-allow3d` from `boot-args`.
2. *(Optional)* Disable the `WhateverGreen.kext` entry if you are using `WhateverXe.kext`.

## Device Properties

Added under `DeviceProperties > Add > PciRoot(0x0)/Pci(0x2,0x0)`:

| Key | Type | Value |
| --- | --- | --- |
| `AAPL,ig-platform-id` | Data | `00005C8A` |
| `device-id` | Data | `528A0000` |
| `framebuffer-patch-enable` | Data | `01000000` |
| `framebuffer-stolenmem` | Data | `00003001` |
| `framebuffer-fbmem` | Data | `00009000` |

- `AAPL,ig-platform-id` is the Ice Lake platform ID `0x8A5C0000`.
- `device-id` spoofs the Xe iGPU as Ice Lake `0x8A52`, because macOS has no native Tiger Lake driver.
- `framebuffer-stolenmem` is 19 MB and `framebuffer-fbmem` is 9 MB.

## Tested Hardware

- HP DW3018NO laptop (mostly works)

## Contributing

Related issues, commits and pull requests are welcome!