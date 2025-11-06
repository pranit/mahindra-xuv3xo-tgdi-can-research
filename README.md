# XUV3XO TGDi (BS6) — ECU PID Reference & CAN Research (Minimal)

This repo contains a **minimal**, research-focused setup to log and decode **Mahindra XUV3XO / XUV300 BS6 1.2 TGDi** ECU PIDs (UDS over CAN).  
**No security bypass** is included. Protected PIDs are readable only when a dealer places the ECU in an **Engineering/Extended Diagnostic Session** (e.g., using K-Diag).

## Contents
- `pids/xuv3xo_pids_with_meanings.csv` — Full PID/DID list with scaling, units, meanings; Protected flagged.
- `can/xuv3xo.dbc` — Minimal DBC mapping for quick decode (UDS responses 0x7E8). See limitations below.
- `tools/analyze_log.ipynb` — Notebook to parse raw CAN logs, decode UDS `0x62` responses, scale values, and plot.
- `docs/obd_splitter_diagram.png` — Wiring reference for OBD Y-splitter setup.
- `docs/savvycan_setup.md` — Basic capture steps with SavvyCAN (works with most USB CAN adapters).

## Quick Start (K-Diag + OBD Splitter)
1. Plug an **OBD Y-splitter** into the vehicle OBD-II port.
2. **Branch A:** Dealer **K-Diag** (they perform authorized engineering session).  
   **Branch B:** Your **CAN logger** (e.g., CANable / PCAN / Kvaser / Vector).
3. Start your logger **before** the dealer enables the session; stop it **after** they end it.
4. Export log as BLF/ASC/CSV. Place file in `logs/` (create if missing).
5. Open `tools/analyze_log.ipynb` and run cells to decode/plot.

### CAN Parameters
- Request ID: `0x7E0`, Response ID: `0x7E8`
- Service: `0x22` (ReadDataByIdentifier), Response: `0x62`
- Bitrate: `500 kbps`

## DBC Notes (Limitations)
`can/xuv3xo.dbc` is a **pragmatic mapping** for UDS `0x62` responses. It decodes simple one/two-byte DIDs assuming responses of the form:  
`62 <DID_hi> <DID_lo> <data...>`  
Because UDS is variable-length and multiplexed by DID, complex multi-frame responses may require the Python notebook decoder (recommended).

## Legal / Safety
- This repository **does not** contain seed→key algorithms or any bypass of ECU security.
- Use **dealer-authorized** engineering sessions for protected PIDs.
- Do not request flashing/calibration changes unless formally authorized.

## Suggested CAN Loggers
- Good: **CANable / CANtact / CandleLight** (with SavvyCAN)
- Pro: **Kvaser Leaf / PCAN-USB / Vector VN1610**
- Not recommended for raw sniffing: Bluetooth ELM-only dongles.

---

Happy researching! Issues/PRs welcome for confirmed PIDs or scaling refinements.
