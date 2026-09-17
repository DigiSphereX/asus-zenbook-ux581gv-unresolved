# Reddit outreach drafts

Ready-to-paste posts for account **u/Happy_Specialist_350**. All English.
Publish them manually on Reddit; this file is a central template you can reuse on any
community.

**Canonical links to reference:**
- Report repository: `https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved`
- GitHub issue (community sign-up): `https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved/issues/1`
- BSOD screenshot (upload directly to the post, do not hotlink): the PNG at
  `ScreenShot/bsod-kernel-security-check-failure-0x139.png`

---

## Before you post (guidelines that actually matter)

1. **Engage first, then post.** If a subreddit has karma/account-age rules, comment
   genuinely for a few days before dropping a link. This is a real community effort, so
   keep the engagement personal.
2. **Upload the screenshot directly to Reddit** so the post gets a thumbnail. Reddit
   cannot hotlink GitHub raw images reliably.
3. **Always disclose the link** is your own GitHub reporting repo — transparency keeps
   the post from being flagged as spam.
4. **Use the right flair** if the sub provides one (e.g. `Support`, `Discussion`,
   `Help`). Set it before posting.
5. **Do not copy-paste the same wall of text into 10 subreddits.** Use the variant that
   fits each community (A/B/C below) and edit the title per sub.
6. **Reply to comments and PMs** — the whole point is to build the user group. Point
   serious owners to the GitHub issue and ask them to confirm/deny the NVMe isolation test.
7. Refresh the post after a few days with a short "update" comment if there is news.

---

## Post A — r/ASUS (primary consumer channel)

**Title (pick one):**

1. `ASUS ZenBook Pro Duo UX581GV dies on current Windows 11 with KERNEL_SECURITY_CHECK_FAILURE (0x139) — no BIOS since 2022, ASUS tooling says hardware is fine`
2. `€2500+ ZenBook Pro Duo UX581GV: endless 0x139 boot loops on every NVMe drive, firmware abandoned since 2022 — gathering owners`
3. `PSA to ZenBook Pro Duo UX581(GV) owners: 0x139 boot loops; drive proven fine elsewhere; ASUS never updated the BIOS`
4. `My UX581GV confirms the drive is NOT the problem (NVMe isolation test) — ASUS is the problem. Any other owners with 0x139?`

**Body (Post A):**

```
TL;DR: My ASUS ZenBook Pro Duo UX581GV (2020, i9-9980HK, RTX 2060, 32 GB) cannot survive
current Windows 11 Pro. Constant KERNEL_SECURITY_CHECK_FAILURE (0x139) blue screens and
endless boot loops. ASUS has shipped NO BIOS since 2022. I ruled out the user, the OS, the
storage and the hardware — with ASUS's own diagnostic tool agreeing the hardware is "fine".

THE DEVICE
- Bought new for more than €2,500 — a flagship creators laptop, effectively premium.
- System drive: 4 TB M.2 NVMe (user-installed). Original 1 TB Samsung OEM drive kept and
  also tested.

SYMPTOMS
- 0x139 BSOD + boot loop after recent Windows 11 Pro updates.
- The same NVMe drive updates and boots perfectly in another PC, and dies again within
  minutes of returning to the ZenBook.
- RTX 2060 severely sluggish under multi-display (ScreenPad Plus + external).
- Persistent mouse stuttering.
- Resident ASUS bloatware stack wasting CPU/RAM/network.

WHAT I ALREADY RULED OUT (all actually tested)
1. Microsoft preview-build theory → 5+ full formats → nothing.
2. Storage → several fresh NVMe drives incl. the original 1 TB Samsung → crash on EVERY
   medium.
3. NVMe isolation test → drive fine in another machine → fails only in this laptop.
4. ASUS MyASUS System Diagnostics → reports NO hardware fault while the machine crashes.
5. Firmware → the official UX581GV support page still lists the 2022 BIOS as the newest.
6. Drivers (GPU/chipset/storage) → updated to newest builds → no change.

CONCLUSION
The fault is the UX581GV platform itself — its BIOS/EC firmware and its Windows 11 driver
contracts, which ASUS refuses to maintain.

CALL TO ACTION
If you own a ZenBook Pro Duo UX581(GV) and see 0x139 (or terrible performance on recent
Windows 11 builds), please comment here or open an issue at the report repository:
https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved/issues/1

We are building a case to escalate to ASUS as a group and request a firmware fix. The
more units reported, the harder it is to ignore.
```

---

## Post B — r/ZenBook / ZenBook Pro Duo owners community

**Title options:**

1. `ZenBook Pro Duo UX581GV owners: 0x139 boot loops on recent Windows 11? Please confirm the NVMe isolation test`
2. `Any UX581(GV) here with KERNEL_SECURITY_CHECK_FAILURE? I proved the drive is fine — testing with other owners`
3. `UX581GV survey: does Windows 11 still crash for you after clean install? (full evidence inside)`

**Body (Post B):**

```
Hey fellow ZenBook Pro Duo owners.

Short version: my UX581GV (i9-9980HK, RTX 2060, 32 GB) keeps blue-screening with
KERNEL_SECURITY_CHECK_FAILURE (0x139) into boot loops on recent Windows 11 Pro, even
after 5+ full formats with different NVMe drives (4 TB aftermarket AND the original 1 TB
Samsung OEM).

The decisive test: I took the exact same 4 TB NVMe system drive, plugged it into a
different computer — it updated and booted perfectly. Back in the ZenBook, it crashes
again within minutes. A drive that works elsewhere cannot be the fault. The platform is.

ASUS's own MyASUS System Diagnostics also reports NO hardware fault. And the official
support page still only offers the 2022 BIOS — there is nothing newer to install.

I also see sluggish RTX 2060 under multi-display and mouse stutter, plus a lot of
unnecessary ASUS background software.

Questions for you:
1. Do you get 0x139 on recent Windows 11 builds?
2. Can you confirm/deny the NVMe isolation test on your unit (drive works fine in
   another machine, fails in the ZenBook)?
3. What BIOS are you on?

I started a small repository to centralize evidence and a call to ASUS:
https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved

Reply here or open an issue if you want to join the group escalation:
https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved/issues/1
```

---

## Post C — r/Windows11 / r/WindowsHelp (platform angle)

**Title options:**

1. `Windows 11 Pro: KERNEL_SECURITY_CHECK_FAILURE (0x139) boot loop on a laptop whose OEM never updated the BIOS — evidence included`
2. `0x139 boot loops on current Windows 11 — is your OEM platform maintenance to blame? (ASUS UX581GV case study)`
3. `Clean-installed Windows 11, healthy 4 TB NVMe (proven in another PC) still crashes on this 2020 ZenBook Pro Duo — stale OEM firmware?`

**Body (Post C):**

```
I want to share a clean case study because it isolates the blame nicely — it is NOT the
user, the OS install, or the drive.

- Machine: 2020 ASUS ZenBook Pro Duo UX581GV (i9-9980HK, RTX 2060, 32 GB), bought for
  €2500+. Runs Windows 11 Pro.
- Failure: KERNEL_SECURITY_CHECK_FAILURE (0x139) blue screens and endless boot loops after
  recent Windows 11 updates. Survives older states, dies after update.
- 5+ full formats, several NVMe drives including the original 1 TB Samsung OEM: crash
  repeats on every medium.
- NVMe isolation: the same 4 TB NVMe system drive updates and boots another PC perfectly;
  returns to the ZenBook → crash again in minutes.
- ASUS MyASUS System Diagnostics: "no hardware fault".
- Firmware: official support page still lists the 2022 BIOS as the newest. Nothing newer.

I can't install a fix that doesn't exist. My read is that a stale OEM BIOS/EC plus
outdated ACPI/ATK drivers can't hold up against current Windows' storage/scheduler
behaviour, and I'd love others to check the same pattern: clean Windows 11 + OEM laptop
with BIOS frozen >2 years.

If you have a UX581(GV) or a similar 2019-2020 premium machine with abandoned firmware
and 0x139, please weigh in — evidence repo here:
https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved

Mini feature request aside: Microsoft Feedback Hub feedback for this class of OEM
firmware staleness would also help, if you're on the Insider program.
```

---

## Post D — follow-up / comment template (short)

Use when replying to comments across all posts:

```
Thanks for the feedback. If it can help, full evidence (screenshots, NVMe isolation test,
ASUS bloatware inventory) is in the report repo: https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved

Please open an issue (https://github.com/DigiSphereX/asus-zenbook-ux581gv-unresolved/issues/1)
with your BIOS build and whether the NVMe isolation test reproduces for you. We're
collecting cases for one collective escalation to ASUS.
```