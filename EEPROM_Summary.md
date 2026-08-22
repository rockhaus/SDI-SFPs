## EEPROM (SFF-8472)

Read with the Ubiquiti SFP Wizard. All three modules assert **10GBASE-LR** compliance and **64B/66B** encoding — neither is true of SDI, which is scrambled NRZI with no line code.

| Field | FS SFP-10GLR-31 | PACBTECH PAC-12G-20 | BMD ADPT-12GBI/OPT |
| ----- | --------------- | ------------------- | ------------------ |
| Vendor Name | FS | `OEM` | PHOTONICSLINK |
| Vendor OUI | `64:9D:99` (FS) | `00:90:65` (**Finisar**) | `00:00:00` (null) |
| Part Number | SFP-10GLR-31 | PAC-12G-20 | PLTG10311**CBMD** |
| Revision | A | A | *(blank)* |
| Compliance | 10G Base-LR | 10G Base-LR | 10G Base-LR |
| Encoding | `0x06` (64B/66B) | `0x06` (64B/66B) | `0x06` (64B/66B) |
| Nominal Bitrate | 10300 MBd | 12000 MBd | 12000 MBd |
| Rate Identifier | `0x00` | `0x00` | `0x00` |
| Link Length (SMF) | 10 km | 20 km | 5 km |
| Wavelength | 1310 nm | 1310 nm | 1310 nm |
| Diag Type | `0x68` | `0x68` | `0x68` |
| Enhanced Opts | `0xF0` | `0xE0` | `0xF0` |
| SFF-8472 Rev | `0x05` (11.0) | `0x03` (10.2) | `0x04` (10.4) |
| Date Code | 2025-03-04 | 2026-03-14 | 2026-04-17 |
| Serial Number | S2512872357 | B0126031094022 | S1224F263000017 |
| CC_BASE / CC_EXT | `0x2D` / `0xE2` — valid | `0xBC` / `0xE5` — valid | `0x6E` / `0x31` — valid |

Notes:

- 12G-SDI is **11.88 Gbps**, which encodes to `0x77` (119) in byte 12 → 11900 MBd. Both "12G" modules report `0x78` (120) → 12000 MBd, a round marketing figure rather than a spec-derived one.
- The PACBTECH carries Finisar's registered OUI with the vendor name string set to the placeholder `OEM` — the signature of a copied EEPROM image.
- The `CBMD` suffix on the Blackmagic-branded module follows the third-party "compatible with BMD" naming convention rather than an OEM part number.
- Bytes 66/67 (BR max / BR min) are `0x00` on all three, so none declares a rate range — none claims coverage down to 270 Mbps SD-SDI.

<details>
<summary><b>FS SFP-10GLR-31</b> — raw output</summary>

```text
File: FS_10G_SFP-10GLR-31.bin (512 bytes)

=== SFP/SFP+ Module (SFF-8472) ===

--- Basic Info ---
Identifier:       0x03 (SFP/SFP+)
Ext Identifier:   0x04
Connector:        0x07 (LC)

--- Transceiver Compliance ---
  - 10G Base-LR
Encoding:         0x06 (64B/66B)
Nominal Bitrate:  10300 MBd
Rate Identifier:  0x00

--- Link Length ---
Single Mode (km): 10 km
Single Mode (m):  10000 m

--- Vendor Info ---
Vendor Name:      FS
Vendor OUI:       64:9D:99
Part Number:      SFP-10GLR-31
Revision:         A
Wavelength:       1310 nm
Serial Number:    S2512872357
Date Code:        2025-03-04 (Lot:   )

--- Diagnostic Monitoring ---
Diag Type:        0x68
  - Digital diagnostics implemented
  - Internally calibrated
  - Received power measurement: average
Enhanced Opts:    0xF0
SFF-8472 Rev:     0x05 (SFF-8472 Rev 11.0)

--- Checksums ---
CC_BASE:          0x2D (VALID)
CC_EXT:           0xE2 (VALID)
```

</details>

<details>
<summary><b>PACBTECH PAC-12G-20</b> — raw output</summary>

```text
File: PACBTECH_PAC-12G-20-SDI.bin (512 bytes)

=== SFP/SFP+ Module (SFF-8472) ===

--- Basic Info ---
Identifier:       0x03 (SFP/SFP+)
Ext Identifier:   0x04
Connector:        0x07 (LC)

--- Transceiver Compliance ---
  - 10G Base-LR
Encoding:         0x06 (64B/66B)
Nominal Bitrate:  12000 MBd
Rate Identifier:  0x00

--- Link Length ---
Single Mode (km): 20 km
Single Mode (m):  20000 m

--- Vendor Info ---
Vendor Name:      OEM
Vendor OUI:       00:90:65
Part Number:      PAC-12G-20
Revision:         A
Wavelength:       1310 nm
Serial Number:    B0126031094022
Date Code:        2026-03-14 (Lot:   )

--- Diagnostic Monitoring ---
Diag Type:        0x68
  - Digital diagnostics implemented
  - Internally calibrated
  - Received power measurement: average
Enhanced Opts:    0xE0
SFF-8472 Rev:     0x03 (SFF-8472 Rev 10.2)

--- Checksums ---
CC_BASE:          0xBC (VALID)
CC_EXT:           0xE5 (VALID)
```

</details>

<details>
<summary><b>Blackmagic ADPT-12GBI/OPT</b> — raw output</summary>

```text
File: Blackmagic-12G-SDI.bin (512 bytes)

=== SFP/SFP+ Module (SFF-8472) ===

--- Basic Info ---
Identifier:       0x03 (SFP/SFP+)
Ext Identifier:   0x04
Connector:        0x07 (LC)

--- Transceiver Compliance ---
  - 10G Base-LR
Encoding:         0x06 (64B/66B)
Nominal Bitrate:  12000 MBd
Rate Identifier:  0x00

--- Link Length ---
Single Mode (km): 5 km
Single Mode (m):  5000 m

--- Vendor Info ---
Vendor Name:      PHOTONICSLINK
Vendor OUI:       00:00:00
Part Number:      PLTG10311CBMD
Revision:         
Wavelength:       1310 nm
Serial Number:    S1224F263000017
Date Code:        2026-04-17 (Lot:   )

--- Diagnostic Monitoring ---
Diag Type:        0x68
  - Digital diagnostics implemented
  - Internally calibrated
  - Received power measurement: average
Enhanced Opts:    0xF0
SFF-8472 Rev:     0x04 (SFF-8472 Rev 10.4)

--- Checksums ---
CC_BASE:          0x6E (VALID)
CC_EXT:           0x31 (VALID)
```

</details>
