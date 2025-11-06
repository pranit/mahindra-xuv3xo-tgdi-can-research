# SavvyCAN Minimal Setup (XUV3XO TGDi)

1. Connect your CAN adapter (CANable/CANtact/PCAN/Kvaser).
2. Bitrate: **500000** (500 kbps).
3. Start capture **before** dealer enables engineering session.
4. File → Save Log as **BLF** (preferred) or **ASC**.
5. Load `can/xuv3xo.dbc` (DBC → Load DBC).
6. For UDS decoding, prefer the Python notebook in `tools/` (it parses `0x62` responses and scales per CSV).
