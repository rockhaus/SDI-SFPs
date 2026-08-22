# 12G-SDI SFP Comparison

Some research I conducted after spending around $400 on a Blackmagic 12G-SDI SFP module and then discovering it works just fine when paired with a $34 FS 10G SFP+ module for networking equipment. These SFPs were installed in a pair of Blackmagic Optical Fiber 12G Miniconverters that support SDI in and out.

**Big caveat:** the connected equipment in my setup only supports 6G-SDI signals. However, other users on Reddit report being able to use the FS 10G SFPs with 12G-SDI signals, and as you will see below, both the BMD and FS SFPs use the same transceiver IC. The actual speed of a 12G-SDI signal is 11.88 Gbps.

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
