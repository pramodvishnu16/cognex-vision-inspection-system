# Cognex Vision Inspection System — Label Verification and Defect Detection

**Vision Platform:** Cognex In-Sight 7000 Series  
**Integration:** EtherNet/IP with Allen Bradley Studio 5000  
**HMI:** FactoryTalk View SE  
**Industry:** Medical Device / Pharmaceutical Manufacturing  

---

## Project Overview

This project demonstrates a production-grade vision inspection system developed using Cognex In-Sight for automated label verification, barcode reading, and defect detection on a pharmaceutical packaging line. The system integrates directly with an Allen Bradley PLC via EtherNet/IP, triggering inspections, reading pass/fail results, and controlling downstream reject handling — all in real time.

The project replicates a real-world medical device manufacturing environment where vision inspection is critical for regulatory compliance and product quality.

---

## System Architecture

```
[Product Enters Inspection Zone]
            |
    [Cognex In-Sight Camera]
            |
   [EtherNet/IP Communication]
            |
  [Allen Bradley Studio 5000 PLC]
       /            \
[Pass: Continue]  [Fail: Reject Gate Activated]
       |
  [FactoryTalk HMI — Live Results]
```

---

## Inspection Jobs

| Job Name | Description |
|---|---|
| `Label_Verify` | Checks label presence, position, and orientation |
| `Barcode_Read` | Reads 1D and 2D barcodes (DataMatrix, Code 128) |
| `Fill_Level_Check` | Verifies fill level within acceptable range |
| `Cap_Presence` | Detects cap presence and correct seating |
| `Defect_Detection` | Identifies surface defects, contamination, foreign objects |

---

## Features

- Cognex In-Sight job development using In-Sight Explorer software
- Label presence, position, and print quality verification
- Barcode and DataMatrix reading using PatMax and IDMax tools
- Fill level inspection using blob analysis and caliper tools
- EtherNet/IP integration with Allen Bradley PLC for trigger and result handshake
- Pass/fail signal output directly to PLC tag for reject gate control
- FactoryTalk View SE HMI displays live camera feed, inspection results, and counters
- Alarm logic for camera offline, trigger timeout, and consecutive fail conditions
- Statistical tracking — pass rate, fail rate, defect category breakdown per shift

---

## Cognex Job Structure

| Tool | Purpose |
|---|---|
| `AcquireImage` | Triggers image capture on PLC signal |
| `PatMax` | Locates label pattern and checks position tolerance |
| `IDMax` | Reads barcode / DataMatrix and verifies content |
| `Blob` | Detects fill level and cap presence |
| `Caliper` | Measures label edge position and dimensions |
| `PassFail Logic` | Combines all tool results into single Pass/Fail output |

---

## PLC Integration — Tag Mapping

| PLC Tag | Type | Description |
|---|---|---|
| `Vision_Trigger` | BOOL | PLC sends trigger to Cognex camera |
| `Vision_Pass` | BOOL | Cognex returns pass result |
| `Vision_Fail` | BOOL | Cognex returns fail result |
| `Vision_Ready` | BOOL | Camera ready for next inspection |
| `Barcode_Data` | STRING | Barcode string read from product |
| `Fail_Count` | DINT | Consecutive fail counter |
| `Reject_Gate` | BOOL | Activates reject diverter on fail |
| `Camera_Fault` | BOOL | Camera offline or communication lost |

---

## HMI Screens

| Screen | Description |
|---|---|
| Vision Overview | Live camera feed, last result, pass/fail indicator |
| Inspection Stats | Pass count, fail count, pass rate percentage |
| Defect Log | Timestamped log of all failed inspections with defect type |
| Camera Setup | Job selection, trigger mode, exposure settings |
| Alarms | Camera faults, consecutive fails, communication errors |

---

## Tools and Technologies

| Category | Tools |
|---|---|
| Vision Software | Cognex In-Sight Explorer |
| PLC Programming | Rockwell Automation Studio 5000 |
| HMI | FactoryTalk View Studio SE |
| Communication | EtherNet/IP |
| Barcode Reading | Cognex DataMan / IDMax |
| Documentation | Inspection Specification, Validation Protocol, Camera Calibration Record |

---

## Setup and Configuration

1. Connect Cognex In-Sight camera to network switch on same subnet as PLC
2. Open In-Sight Explorer and assign camera IP address
3. Load inspection job `Label_Verify.job` from the `/jobs` folder
4. In Studio 5000, configure EtherNet/IP adapter for Cognex camera
5. Map PLC tags to Cognex I/O assembly per `IO_Mapping.xlsx`
6. Set trigger mode to **External Trigger** driven by PLC conveyor index signal
7. Run calibration routine and verify pass/fail thresholds
8. Test with known good and known bad samples before production use

---

## Validation and Compliance

This inspection system was designed with FDA 21 CFR Part 11 and GMP manufacturing requirements in mind:

- All inspection results logged with timestamp and product ID
- Camera calibration records maintained per shift
- Defect images saved automatically for traceability
- Alarm escalation for consecutive failures requiring operator intervention
- FAT and SAT protocols included in documentation folder

---

## Project Documentation

| Document | Description |
|---|---|
| `IO_Mapping.xlsx` | EtherNet/IP tag mapping between Cognex and PLC |
| `Inspection_Spec.pdf` | Vision inspection specification and acceptance criteria |
| `Validation_Protocol.pdf` | IQ/OQ/PQ validation protocol template |
| `Calibration_Record.pdf` | Camera calibration and verification record |
| `FAT_Checklist.pdf` | Factory Acceptance Test checklist |

---

## About

Developed by **Pramod Vishnumolakala**  
Controls and Systems Engineer | Allen Bradley | Cognex Vision | FactoryTalk | Fanuc  
Location: Moraine, OH  
LinkedIn: linkedin.com/in/pramodvishnumolakala  
Email: pramodvishnu16@gmail.com

---

## Related Skills

`Cognex In-Sight` `Vision Inspection` `PLC Programming` `Studio 5000` `EtherNet/IP` `FactoryTalk View` `Label Verification` `Barcode Reading` `Industrial Automation` `Medical Device Manufacturing` `FDA GMP` `Quality Control`
