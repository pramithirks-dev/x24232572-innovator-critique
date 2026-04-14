# Prototype & Design Specs — GajaLens Sentinel Pod v0.3

## Industrial Design

### Sentinel Pod (ground station)
- **Form factor**: 600 mm × 600 mm × 1100 mm tapered hexagonal column
- **Material**: recycled marine-grade aluminium body, IP67 sealed, UV-stabilised polycarbonate dome
- **Colour**: matte forest green (#1E3D2F) with copper accents (#B87333) — blends into plantation canopy
- **Mounting**: ground anchor (M16 expansion bolts) or 3-point tree strap
- **Weight**: 24 kg
- **Power**: 220 W bifacial solar panel + 2.5 kWh LiFePO₄ battery (5 days autonomy in monsoon)

### Companion Drone — "Karuna" (means *compassion*)
- **Type**: tethered quadcopter, 380 mm motor-to-motor
- **Tether**: 200 m Kevlar-reinforced fibre-optic + power line
- **Payload**: 4K RGB + 640×512 thermal + 360° mic array
- **Endurance**: continuous (tethered power)
- **Acoustic deterrent**: parametric speaker, 15–35 Hz infrasound + 20 Hz "bee swarm"
- **Flight modes**: Auto-Patrol, Investigate, Shadow, Return-to-Dock

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│             FARMER PHONE (WhatsApp/SMS)             │
└─────────────────────────────────────────────────────┘
                          ▲
                          │ alerts
                          │
┌─────────────────────────────────────────────────────┐
│   GajaNet Cloud  ◄────  4G / LoRa Mesh Uplink       │
│   (PostgreSQL +                                     │
│    PostGIS +                                        │
│    Conflict API)                                    │
└─────────────────────────────────────────────────────┘
                          ▲
                          │
┌─────────────────────────────────────────────────────┐
│           SENTINEL POD  (edge)                      │
│  ┌──────────────────────────────────────────────┐   │
│  │ Jetson Orin Nano │ YOLO-v9 elephant model    │   │
│  │ 8 GB             │ Re-ID embedding (FaceNet) │   │
│  └──────────────────────────────────────────────┘   │
│         ▲                              ▲            │
│         │ video + thermal              │ audio      │
│  ┌──────┴──────────┐         ┌─────────┴────────┐   │
│  │  Karuna Drone   │         │ Acoustic Array   │   │
│  │  (tethered)     │         │ (infrasound)     │   │
│  └─────────────────┘         └──────────────────┘   │
└─────────────────────────────────────────────────────┘
```

## AI Model Specs

| Component | Model | Dataset | Target metric |
|---|---|---|---|
| Detection | YOLOv9-c (quantised INT8) | 80k labelled frames (WTI + iNaturalist + own captures) | mAP50 ≥ 0.94, latency ≤ 35 ms on Jetson |
| Re-identification | ArcFace embedding head | 1,200 individual elephants, 18k crops | Rank-1 ≥ 0.87 |
| Behaviour classifier | Temporal CNN (3D ResNet-18) | 6k 5-sec clips | Charge / Foraging / Walking / Calf-present, F1 ≥ 0.82 |
| Acoustic trigger policy | Contextual bandit (Thompson sampling) | online | habituation rate < 8% / 90 days |

## Key Specs Summary

| Spec | Value |
|---|---|
| Detection range (thermal) | 220 m |
| Detection range (RGB, daylight) | 350 m |
| First-alert latency | < 4 seconds |
| Coverage per pod | 4 hectares |
| Battery autonomy (no sun) | 5 days |
| Operating temperature | −5 °C to +55 °C |
| Connectivity | 4G LTE Cat-4 + LoRa fallback |
| Cost-to-build (BOM, v0.3 small batch) | ₹78,500 (~US $940) |
| Target retail BOM at 10k units | ₹38,000 (~US $455) |
| Subscription | ₹499 / month |

## v0.3 Bill of Materials (excerpt)

| Item | Qty | Unit Cost (₹) |
|---|---:|---:|
| Jetson Orin Nano 8 GB | 1 | 22,500 |
| Tethered drone frame + ESC + motors | 1 | 18,000 |
| Thermal core (FLIR Lepton 3.5) | 1 | 14,500 |
| 220 W bifacial solar panel | 1 | 6,800 |
| 2.5 kWh LiFePO₄ pack | 1 | 9,200 |
| Parametric speaker array | 1 | 4,300 |
| Enclosure (machined Al + dome) | 1 | 3,200 |
| **Total v0.3** |  | **78,500** |

## Field Test Plan (90-day pilot)
- **Site**: 12 smallholder coconut farms, Wayanad, Kerala
- **Partner**: Kerala Forest Department + Wildlife Trust of India
- **Primary KPI**: incidents of crop entry per pod-night (baseline vs. deployment)
- **Secondary KPI**: farmer NPS, elephant stress proxy (heart rate via thermal vibrometry on collared individuals)
- **Ethical review**: cleared by NCBS Institutional Animal Ethics Committee
