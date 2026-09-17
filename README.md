# Unresolved System Instability & Hardware Neglect — ASUS ZenBook Pro Duo (UX581GV)

![Status: Open](https://img.shields.io/badge/status-open-orange)
![Device](https://img.shields.io/badge/device-ASUS%20UX581GV-blue)
![OS](https://img.shields.io/badge/OS-Windows%2011%20Pro-informational)
![BIOS support](https://img.shields.io/badge/BIOS-support%20ended%202022-critical)

> Documenting a persistent, critical failure that ASUS has **not** fixed and shows no
> sign of fixing. This repository is the community hub for owners of the ZenBook Pro Duo
> (UX581GV) who experience the same issues, so we can escalate a **collective complaint**
> to ASUS and demand a firmware resolution.

---

## ملخص بالعربية (Arabic summary)

- الجهاز: **ASUS ZenBook Pro Duo UX581GV** (معالج Intel Core i7/i9 من الجيل التاسع، RTX 2060،
  ScreenPad Plus، ويندوز 11 Pro).
- المشكلة: شاشة موت زرقاء متكررة **KERNEL_SECURITY_CHECK_FAILURE (0x139)** تؤدي إلى
  حلقة إقلاع لا تنتهي، حتى بعد إعادة تهيئة النظام عدة مرات.
- الدليل الأهم: القرص NVMe عند عزله ووصلته بجهاز آخر يعمل **بنجاح** ويتم التحديث والإقلاع
  بشكل طبيعي، لكنه يفشل فوراً عند إعادته إلى هذا الجهاز — أي أن الخلل في الجهاز/الفرموير وليس في القرص.
- بالإضافة إلى: أداء ضعيف لكرت الشاشة RTX 2060، وارتعاش مستمر في الماوس، وبرامج ASUS
  كثيرة تعمل في الخلفية وتستهلك الموارد، وASUS لم تُصدر أي تحديث BIOS منذ 2022 (تخلي عن الدعم).
- الهدف: تجميع المستخدمين المتأثرين لعمل شكوى جماعية لـ ASUS. شارك عبر GitHub Issues.

---

## The problem

After multiple full system formats and fresh Windows 11 Pro installations, the machine
crashes into endless boot loops with **`KERNEL_SECURITY_CHECK_FAILURE (0x139)`** whenever
it is updated to recent Windows 11 Pro builds.

![KERNEL_SECURITY_CHECK_FAILURE (0x139) blue screen](https://raw.githubusercontent.com/DigiSphereX/asus-zenbook-ux581gv-unresolved/main/ScreenShot/bsod-kernel-security-check-failure-0x139.png)

- **`0x139`** means the kernel detected corruption of a security-critical data structure
  (so-called *"kernel pool corruption"* family). It points to **firmware/driver/memory
  disruption**, not to a dead disk.
- The behavior is **unstable under current Windows builds** and is not reproducible as a
  standard hardware-DOA: the machine runs older states fine, then dies after update.

## Key evidence — the NVMe isolation experiment

This is the most important clue we have:

| Test | Result |
|---|---|
| System on the UX581GV, current Windows 11 build | **Crash (0x139), boot loop** |
| The same NVMe drive alone in another machine | **Update + boot complete successfully** |
| The same drive returned to the UX581GV | **Fails again immediately** |

A drive that is healthy enough to update and boot another PC does not die on return —
unless the *host machine* (BIOS/EC firmware, ACPI/ATK driver stack, NVMe firmware interplay,
or a storage/NVMe driver regression on this specific platform) is what kills it.

**Conclusion:** the fault lives in the ZenBook Pro Duo platform (firmware/driver), not in
the user, the OS install, or (most likely) the NVMe unit itself.

## Symptoms

1. **Constant `0x139` BSODs** and endless boot loops after recent Windows 11 Pro updates.
2. **NVMe isolation test** — drive updates and boots on another machine, fails only in the ZenBook.
3. **Severe RTX 2060 sluggishness** during multitasking / multi-display
   (ScreenPad Plus + external monitors) workloads.
4. **Persistent, disruptive mouse stuttering**.
5. **High resource consumption by unnecessary ASUS background processes**
   (full list below).

## Manufacturer status

- **No BIOS update since 2022** for UX581GV. Premium hardware officially on the shelf.
- No firmware fix for the `0x139` crash class, no public acknowledgement, no timeline.
- Ticket-level support on ASUS forums produces generic advice only (reinstall, update
  drivers that are themselves outdated).

ASUS effectively **abandoned hardware support** on this model, leaving several
thousand premium machines unstable on supported Windows builds.

---

## ASUS software consuming resources — what is unnecessary

One part of this is self-inflicted: ASUS preloads a stack of resident background software
that does very little for everyday work while consuming CPU, RAM, disk, and network.

> ⚠️ **Safety:** uninstall/disable only the *applications and services* — keep the ASUS
> **drivers** (ATK ACPI, touchpad, keyboard, ScreenPad+, graphics). Disabling hotkey/ACPI
> *services* may remove function-key behaviour on some models; you can set them to
> **Manual** instead of Disabled.

| Program / service | Main processes | What it does | Resource pressure | Verdict |
|---|---|---|---|---|
| **MyASUS** | `MyASUS.exe`, `asusservice.exe` | Support portal, driver/BIOS updater, system diagnostics | Medium (resident + auto-updates) | Optional — keep only if you use it; disable *auto-update* / *background* |
| **Armoury Crate** | `ArmouryCrate.exe`, `ArmouryCrateService.exe`, `ASUSAppService.exe` | RGB, performance/AURA profiles (Electron-based, heavy) | High on low-power CPUs | **Uninstall if you do not need RGB/performance profiles** |
| **ROG Live Service** | `rog_live_service.exe` | Game/ROG app updater service | Medium | Unnecessary for non-gaming / can disable |
| **ASUS LiveUpdate** | `LiveUpdate.exe`, "ASUS Update" | Scheduled updater | Medium | **Disable** — rarely needed, updates already handled by MyASUS |
| **ASUS System Control Interface** | driver service (ASUS SCI) | Supports MyASUS/Armoury hardware calls | Low, resident | Keep the **driver**; no disable needed |
| **ATK Package (ASUS Hotkeys)** | `asussvc.exe`, `atkexComSvc.exe`, `HControl.exe` | Hotkey (Fn) handling, brightness/volume OSD | Low (tray resident `HControl.exe`) | Keep driver; `HControl.exe` tray can be disabled from Startup |
| **ASUS Smart Display Control / ASUS Switch** | `asmMgr.exe`, `swp.exe` | ScreenPad+ (second touch screen) manager | Medium | Needed only if you use ScreenPad+; harmless to stop the *app* |
| **ASUS GameVisual** | `GameVisual.exe` (+ service) | Display colour/preset profiles | Medium | **Disable** unless you use presets |
| **ASUS Optimization** | `ASUSOptimization.exe` (older models) | "Optimization" so-called features | Medium | **Disable** — historically resource-hungry, few benefits |
| **ASUS Promotion / Product Improvement Program** | background | Telemetry + promotional content | Low but pointless | **Turn OFF** (MyASUS settings) or uninstall |
| **ASUS Framework Service** | `ASUSLinkAccount.exe` | ASUS account integration | Medium | **Uninstall** — not needed to use the laptop |
| **ASUS WiFi Radar** | UWP app (legacy) | WiFi utilities/search | Medium | **Uninstall** |
| **eSupport / ASUS Smart Guide / ASUS Online Update** | `eSupport.exe` etc. | Help/recovery bloat | Low | **Uninstall** |

### How to identify what is actually running on *your* machine

PowerShell (no admin needed for processes; admin for services):

```powershell
# Resident processes from the ASUS family, sorted by RAM use
Get-Process | Where-Object { $_.Name -match 'asus|armoury|rog|atk|myasus|hcontrol|liveupdate|gamevisual|swp|asm|esupport' } |
    Sort-Object WorkingSet64 -Descending |
    Select-Object Name, Id, CPU, @{n='RAM(MB)';e={[math]::Round($_.WorkingSet64/1MB,1)}}, Path

# ASUS services and their state (elevated to change them)
Get-Service | Where-Object { $_.DisplayName -match 'ASUS|ROG|Armoury|ATK|LiveUpdate|GameVisual|Switch' } |
    Select-Object Status, StartType, Name, DisplayName

# Startup entries
Get-CimInstance Win32_StartupCommand | Where-Object { $_.Command -match 'asus|armoury|rog' } |
    Select-Object Name, Command
```

Typical result on a UX581GV: **6–12 ASUS processes resident**, often 300–900 MB RAM combined
plus constant disk/network activity — on a machine that is dying from `0x139` boot loops,
that is a measurable share of the resource contention.

---

## Diagnostics performed so far

- [x] Multiple **full formats + clean Windows 11 Pro installs** — crash persists on current builds.
- [x] **NVMe isolation test** on a second machine — drive works; fails only in the ZenBook.
- [x] Updated graphics/nvme/chipset drivers to newest available — no change.
- [x] No vendor firmware fix available (last BIOS 2022).

## Suspected root cause

Given the evidence, the most probable contributors, in order:

1. **Stale ASUS BIOS/UEFI + EC firmware (2022)** incompatible with recent Windows 11
   storage/scheduler behaviour → storage-stack corruption under load → `0x139`.
2. **ASUS ACPI/ATK + System Control Interface drivers** shipped for the model never
   updated for Windows 11 → service/driver interference.
3. **dGPU (RTX 2060) power-management bug** on this platform under multi-display
   (ScreenPad+ + external) → sluggishness, possible PCIe/display interference.
4. Resident **ASUS bloatware stack** raising background load and triggering the failure
   class earlier than it would otherwise appear.

None of these can be fixed on the user side beyond workarounds — the firmware fixes are
ASUS's responsibility.

## How you can help (community)

Owners of **ZenBook Pro Duo UX581 (UX581GV)** (and related UX581 family):

1. **Open a GitHub Issue** in this repository describing your case (customs, build,
   first crash date, current BIOS).
2. Attach diagnostic facts:
   - `winver` build + BIOS version
   - Last BSOD: **`!analyze -v`** output from WinDbg on `C:\Windows\Minidump\*.dmp`
     (we care about the **`Probably caused by:`** line and the `0x139 (param1..param4)` values)
   - **Event Viewer**: `Kernel-Power 41`, `WHEA-Logger`, `nvme`/`storport` errors
3. Confirm/deny the **NVMe isolation result** on your unit.
4. Vote/comment — the more of us, the stronger the escalation.

We are forming a **user community** to escalate a collective complaint and demand a
firmware resolution from ASUS.

**Contact:** open an Issue above, or start a Discussion. Let's get ASUS to respond.

---

## Disclaimer

This repository is an independent user effort. It is **not** affiliated with, endorsed by,
or supported by ASUSTeK Computer Inc. Information here is shared in good faith for
diagnostic purposes; apply changes at your own risk.

## License

The report and materials in this repository are provided under
[CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) (public domain) so the
information can circulate freely in the fight for a fix.