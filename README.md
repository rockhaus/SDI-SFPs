# 12G-SDI SFP Comparison

Some research I conducted after spending around $400 on a Blackmagic 12G-SDI SFP module and then discovering it works just fine when paired with a $34 FS 10G SFP+ module for networking equipment or with PACBTECH 12G-SDI SFPs. These SFPs were installed in a pair of Blackmagic Optical Fiber 12G Miniconverters that support SDI in and out.

**Big caveat:** the connected equipment in my setup only supports 6G-SDI signals. However, other users on Reddit report being able to use the FS 10G SFPs with 12G-SDI signals, and as you will see below, both the BMD and FS SFPs use the same transceiver IC. The actual speed of a 12G-SDI signal is 11.88 Gbps.

I have also included EEPROM dumps for three of the SFPs using Ubiquiti's SFP Wizard at then end of the page.

<img src="images/blackmagic-mini-converter-optical-fiber-12g.jpg" alt="Blackmagic Mini Converter Optical Fiber 12G" width="500">

## Summary

| Make     | Model            | Transceiver IC     | Advertised Max Speed of IC | Cost  |
| -------- | ---------------- | ------------------ | -------------------------- | ----: |
| Neton    | NTX-8D32HJ-1310  | [MACOM M02193](https://www.macom.com/products/product-detail/M02193)  | 12.5 Gbps                  | ??    |
| PACBTECH | PAC-12G-20       | [MACOM M02193](https://www.macom.com/products/product-detail/M02193)  | 12.5 Gbps                  | ~$70  |
| BMD      | ADPT-12GBI/OPT   | [Gennum GN1157](https://www.semtech.com/products/signal-integrity/laser-drivers-transceivers/gn1157)      | 11.3 Gbps                  | ~$465 |
| FS       | SFP-10GLR-31     | [Gennum GN1157](https://www.semtech.com/products/signal-integrity/laser-drivers-transceivers/gn1157)      | 11.3 Gbps                  | ~$34  |

[^1]: Top marking partially obscured; identified by comparison with the Neton module's `02193G12 / 2029 MY` marking.

It can be seen in the teardown photos that the BMD SFP does have larger capacitors than the other SFPs, however the IC is not rated for the speeds that 12G-SDI requires.

## Neton NTX-8D32HJ-1310

MACOM M02193

Secondary IC: PA8Z2 (6-pin)

<img src="images/neton-ntx-8d32hj-1310-module-and-label.jpg" alt="Neton NTX-8D32HJ-1310 module and label" width="800">

<img src="images/neton-ntx-8d32hj-1310-board-m02193.jpg" alt="Neton board showing the MACOM M02193" width="800">

## PACBTECH PAC-12G-20

MACOM M02193

<img src="images/pacbtech-pac-12g-20-label.jpg" alt="PACBTECH PAC-12G-20 label" width="800">

<img src="images/pacbtech-pac-12g-20-module-open.jpg" alt="PACBTECH PAC-12G-20 with cover removed" width="800">

<img src="images/pacbtech-pac-12g-20-board-and-cover.jpg" alt="PACBTECH PAC-12G-20 board and cover" width="800">

## FS SFP-10GLR-31

Gennum (now Semtech) GN1157 — LR transceiver chip. 

MCU: F850I

<img src="images/fs-sfp-10glr-31-module-and-label.jpg" alt="FS SFP-10GLR-31 module and label" width="800">

<img src="images/fs-sfp-10glr-31-board-gn1157-side.jpg" alt="FS board, GN1157 side" width="800">

<img src="images/fs-sfp-10glr-31-gn1157-closeup.jpg" alt="Close-up of the Gennum GN1157 in the FS module" width="800">

<img src="images/fs-sfp-10glr-31-gn1157-detail.jpg" alt="Detail of the GN1157 top marking in the FS module" width="800">

## Blackmagic ADPT-12GBI/OPT

Gennum (now Semtech) GN1157 —  LR transceiver chip. 

MCU: SIL F336

Has larger caps and inductors compared to the others.

<img src="images/blackmagic-adpt-12gbi-opt-label.jpg" alt="Blackmagic 12G Transceiver label" width="800">

<img src="images/blackmagic-adpt-12gbi-opt-board-gn1157-side.jpg" alt="Blackmagic board, GN1157 side" width="800">

<img src="images/blackmagic-adpt-12gbi-opt-board-mcu-side.jpg" alt="Blackmagic board, MCU side" width="800">

## BMD vs FS

Same transceiver IC, different board build. Larger caps and inductors on the BMD board.

| BMD | FS |
| :---: | :---: |
| <img src="images/blackmagic-adpt-12gbi-opt-board-mcu-side.jpg" alt="BMD board, MCU side" width="420"> | <img src="images/fs-sfp-10glr-31-board-mcu-side.jpg" alt="FS board, MCU side" width="420"> |
| <img src="images/blackmagic-adpt-12gbi-opt-board-gn1157-side.jpg" alt="BMD board, GN1157 side" width="420"> | <img src="images/fs-sfp-10glr-31-board-gn1157-side.jpg" alt="FS board, GN1157 side" width="420"> |


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
