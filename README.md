# Acer Nitro V15 — Windows 11 Clean Install & WiFi Driver Fix (MediaTek MT7921)

A troubleshooting reference for fixing a corrupted Windows install and restoring WiFi/touchpad drivers after a clean install — especially useful if your WiFi chip is a **MediaTek MT7921**.

## The Problem

Symptoms before the fix:
- Cursor stuck in a constant spinning "loading" state
- Microsoft Word/Excel wouldn't open
- Windows activation failing with a KMS error

## The Fix — Step by Step

### 1. Clean Windows 11 Install
- Created a bootable USB (Ventoy had issues → used **Rufus** instead, which worked reliably)
- Backed up important files first (documents, projects, photos, videos)
- Installed Windows 11 fresh
- Bypassed the mandatory internet requirement during setup

### 2. Post-Install Problem: No WiFi, No Touchpad, No Internet
- Fresh install had no network drivers installed
- No internet meant no direct driver downloads *on that machine*
- **Workaround:** downloaded drivers on a separate laptop → transferred via USB pendrive → repeated multiple times as different driver attempts failed

**[IMAGE PLACEHOLDER — Device Manager with yellow-warning icon on an unknown device]**

### 3. The Breakthrough: Find the Exact Hardware ID

Instead of guessing drivers based on laptop model, check the exact hardware ID:

`Device Manager → Network adapters → [device] → Properties → Details tab → Hardware Ids`

Result: **PCI\VEN_14C3&DEV_7961**

- `VEN_14C3` = MediaTek
- `DEV_7961` = MT7921 (WiFi chip)

**[IMAGE PLACEHOLDER — Hardware Ids dropdown screenshot]**

### 4. Correct Driver Source

Search using the hardware ID or chip name — **not** the laptop model:
> "MediaTek MT7921 Windows 11 driver"

✅ Working driver found here:
[DriversCloud — MediaTek MT7921 WLAN Driver](https://www.driverscloud.com/en/services/GetInformationDriver/76409-0/mediatek-mediatek-wlanv3401063zip)

## Is This Driver Laptop-Specific?

No — it's tied to the **hardware chip**, not the laptop brand or model.

| Laptop | WiFi Chip | Compatible? |
|---|---|---|
| Acer Nitro V15 | MediaTek MT7921 | ✅ Yes |
| ASUS TUF (MT7921) | MediaTek MT7921 | ✅ Yes |
| Lenovo Legion (AX211) | Intel AX211 | ❌ No |
| HP Victus (RTL8852BE) | Realtek | ❌ No |

## Post-Fix Checklist

- [ ] Run Windows Update repeatedly (2–4 rounds) — picks up touchpad, Bluetooth, audio, chipset drivers
- [ ] Check Device Manager for remaining yellow-warning devices
- [ ] Install NVIDIA driver directly from NVIDIA (for dedicated GPU laptops)
- [ ] Optional: install Acer NitroSense / Acer Care Center
- [ ] Confirm Windows activation (Settings → System → Activation)
- [ ] Restore backed-up files

## Key Lessons

1. **Always find the exact Hardware ID before searching for a driver.** Model-based searches are unreliable — the same model can ship with different components.
2. **Keep a backup driver folder** (WiFi, touchpad, audio, LAN, Bluetooth, chipset, GPU) so future reinstalls take minutes, not hours.
3. Manual USB-based driver transfers are painful but work — expect several hit-and-trial rounds if you don't have a second internet-connected route.

## Who This Helps

Anyone who:
- Just did a clean Windows install and lost WiFi/touchpad
- Has a MediaTek MT7921 wireless chip specifically
- Wants a repeatable method for identifying unknown hardware after any Windows reinstall

---

*Maintained by **Anish Jha** | [Medium](https://medium.com/@anishjha032) | [LinkedIn](https://linkedin.com/in/anish-jha-b49367330)*
