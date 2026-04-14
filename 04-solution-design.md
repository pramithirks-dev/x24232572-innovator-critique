# Solution Design — GajaLens

## Provider
**GajaLens Technologies Pvt. Ltd.** — a for-profit conservation-tech startup headquartered in Bengaluru with a field operations base in Wayanad, Kerala. Co-founded by a wildlife biologist (ex-Wildlife Trust of India), a computer-vision engineer (ex-NVIDIA), and a rural-finance specialist (ex-Kudumbashree). Hybrid model: revenue-generating service for farmers + grant-funded co-deployment with state forest departments.

## The Offering — Hybrid Hardware + Service

### 1. Hardware: The GajaLens Sentinel Pod
A solar-powered, weather-sealed perimeter station containing:
- **Tethered AI drone** (returns to dock, charges in 18 min, 200 m operational radius)
- **Edge-AI vision module** (NVIDIA Jetson Orin Nano, runs YOLO-v9 trained on 80,000 elephant images)
- **Multi-spectral acoustic deterrent array**: low-frequency rumble (15–35 Hz), bee-buzz playback, ultrasonic pulses
- **Thermal + LIDAR sensor fusion** (operates in zero-light, monsoon fog)
- **4G/LoRa mesh uplink** (works in connectivity-dead zones)

### 2. Service: GajaLens Guardian (subscription)
- **₹499/month** for a 2-hectare plot (one Sentinel Pod covers up to 4 ha)
- 24/7 monitoring, SMS/WhatsApp alerts in Malayalam, Kannada, Tamil
- Insurance-backed crop-loss guarantee (underwritten by partner: ICICI Lombard)
- Free hardware swap, OTA software updates
- Shared "herd cards" — each elephant individually re-identified and named, building community trust

### 3. Data Layer: GajaNet
Anonymised herd movement data sold (with state consent) to forest departments and conservation NGOs as a **Conflict Heatmap API**, funding the subsidised farmer tier.

## How It Works (User Journey)
1. **Dusk** — Sentinel Pod auto-launches drone for perimeter sweep
2. **Detection** — Edge-AI flags an elephant 180 m out, classifies herd size, identifies individuals
3. **Graduated response**:
   - Stage 1: low-frequency rumble (mimics bull warning)
   - Stage 2: bee-buzz playback (proven aversive — Lucy King, Save the Elephants)
   - Stage 3: SMS to farmer + alert to nearest forest range officer
4. **Logging** — encounter is added to GajaNet for the corridor
5. **Dawn** — drone returns to dock; farmer receives a respectful, beautiful photo of last night's visitor

## Why It Wins
- **Non-lethal & culturally aligned** — elephants are sacred to Hindu and Buddhist communities; killing solutions are politically toxic
- **Cheaper than fencing** — solar electric fence: ₹1.2 lakh / km install + ₹15k/yr maintenance vs. ₹6k/yr GajaLens subscription
- **Insurable** — first HEC solution to bundle a financial guarantee
- **Dual-purpose data** — same hardware that protects farms feeds national conservation science
