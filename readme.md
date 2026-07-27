# Google Home Automations

A collection of custom YAML scripts for the Google Home Script Editor ([home.google.com](https://home.google.com)).

## Repository Structure

| File | Description | Status |
| :--- | :--- | :--- |
| `circadian-lighting.yml` | 6-stage time and presence-based colour temperature and brightness manager. | Active |

---

## Active Scripts

### 1. Circadian, Wake & Sleep Routine (`circadian-lighting.yml`)

Automates lighting adjustments across the day to match natural circadian rhythms, moving from cooler light in the morning to low-blue warm tones in the evening.

#### Schedule

| Time | Stage | Temperature | Brightness | Action / Effect |
| :--- | :--- | :--- | :--- | :--- |
| **06:00** | Morning Wake | Dynamic | 0% → 100% | `LightEffectWake` (30 min transition) |
| **09:00** | Daytime Focus | `4200K` | `90%` | Crisp neutral light for daytime activity |
| **14:30** | Afternoon Taper | `3800K` | `70%` | Slight drop in intensity and warmth |
| **17:30** | Evening Wind-Down | `2800K` | `40%` | Warm ambient light |
| **20:00** | Night Relax | `2200K` | `20%` | Low-blue tone prior to sleep |
| **21:00** | Bedtime Sleep Effect | Dynamic | 20% → 0% | `LightEffectSleep` (30 min transition) |

#### Rules & Constraints
* **Presence Check:** Every automation block requires `home.state.HomePresence` to be `HOME`. Scheduled state changes will not trigger or turn on lights when the house is empty.
* **Target Devices:**
  * `Bedroom lamp - Bedroom`
  * `Office lamp - Office`
  * `Living Room floor lamp - Living Room`
  * `Living Room table lamp - Living Room`

---

## Maintenance & Deployment Notes

* **Device Mapping:** If smart lamps are renamed or moved to different rooms in the Google Home app, update the array under `devices:` in the YAML block to match the exact `Device - Room` format.
* **Editor Warnings:** `home.state.HomePresence` triggers an advisory warning in the web editor regarding presence signals. This does not prevent script validation or execution.