# SDI-SFPs

Some research I conducted after spending around $400 on a Blackmagic 12G-SDI SFP module and then discovering it works just fine when paired with a $34 FS 10G SFP+ module for networking equipment. These SFPs were installed in a pair of Blackmagic Optical Fiber 12G Miniconverters that support SDI in and out. Big caveat: The connected equipment in my setup only supports 6G-SDI signals. However, other users on Reddit report being able to use the FS 10G SFPs with 12G-SDI signals, and you will see below, that both the BMD and FS SFPs use the same transceiver IC. The actual speed of a 12G-SDI signal is 11.88 Gbps.

| Make     | Model             | Transceiver IC | Advertised Max Speed of IC | Cost   |
| :-------- | :----------------- | :-------------- | :-------------------------- | ------: |
| Neton    | NTX-8D32HJ-1310   | MACOM M02193   | 12.5 Gbps                  | ??     |
| PACBTECH | PAC-12G-20        | MACOM M02193   | 12.5 Gbps                  | ~$70   |
| BMD      | ADPT-12GBI/OPT    | Gennum GN1157  | 11.3 Gbps                  | ~$465  |
| FS       | SFP-10GLR-31      | Gennum GN1157  | 11.3 Gbps                  | ~$34   |


It can be seen in the teardown photos, that the BMD SFP does have larger capacitors than the other SFPs, however the IC is not rated for the speeds that 12G-SDI requires.
