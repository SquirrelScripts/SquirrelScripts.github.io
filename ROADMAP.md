# SquirrelScripts — Roadmap 🐿️

> A small, trusted stash of Windows tools sysadmins actually reach for. Quality over quantity — every script earns its card or it doesn't ship.

---

## The squirrel rules

Non-negotiables. A tool that breaks one of these isn't a SquirrelScript.

1. **Preview before the deed.** Default to `-WhatIf` / a dry run. People should always see what a tool *will* do before it does it. This is the signature — it's what separates the stash from an AI-generated script dump.
2. **Never hurt the user.** Safe defaults, reversible where possible, no force-closing apps, no destructive surprises. Touch only what regenerates.
3. **Satisfying finish.** End with the number — `Freed 2.3 GB`, `Found 14 stale accounts`. The flush moment.
4. **Single file, low friction.** One `.ps1`, no dependencies, no admin for the default path where it's avoidable. Runs straight off a download (with `Unblock-File`).
5. **Maintained beats many.** Cap the stash around 10–15. If it can't be kept working, it doesn't belong on the shelf.

Rules 1–3 and 5 are the brand and apply to everything with the squirrel on it. Rule 4 is script-specific — see [the workshop](#the-workshop) for how apps read it.

---

## The stash

### ✅ Shipped
- **SquirrelCleaner** — quick Windows cache cleaner. User temp + browser caches by default, opt-in system/Windows Update/recycle bin. `-WhatIf` first, won't kill your browser.
- **Disk-Hog Finder** (`Get-SquirrelHogs`) — drive free space, biggest folders, top-N largest files. Read-only — reports, never deletes. Junction- and OneDrive-aware so the numbers are honest. Pairs with the cleaner (find hogs → clean).
- **Network Repair Kit** (`Repair-SquirrelNet`) — diagnoses first, then a gentlest-first repair ladder (DNS flush → re-register → DHCP renew → adapter restart), re-testing after each step and stopping the moment it's back. Winsock/TCP-IP resets opt-in via `-Deep` with explicit warnings; state snapshotted to a receipts file before anything runs.

### 🔜 Next up — *free lane* (build these next, same lane as the cleaner)

Free lane complete — all three shipped. Reassess here: nail the existing three, gather feedback/traction, then decide between the "maybe" items and the paid lane.

### 🤔 Maybe / smaller
- [ ] **Targeted cache nuke** — Teams/Outlook "app won't load, clear its cache." Useful, but probably a *mode* of SquirrelCleaner rather than its own card. Revisit.
- [ ] **Windows debloat / fresh-install setup** — high traffic but crowded (Win11Debloat et al.) and higher risk. Only worth it as the safe, reversible, preview-first take. Park it.

### 🔒 Later — *paid lane* (the module / upsell, not day-one free)
Higher value, different audience (AD / M365 admins), more maintenance, needs a domain or tenant to test. This is where people actually pay — lifecycle packs sell for $15–$49. Save these for the "install the whole stash" module.

- [ ] **Stale/Inactive AD Account Finder + Disabler** — `Search-ADAccount -AccountInactive` → report, then optionally disable (with `-WhatIf`, naturally). Security + compliance value, recurring.
- [ ] **User Offboarding (AD + M365)** — disable account, reset password, strip groups, convert mailbox to shared, revoke sessions. The single most-requested and most-monetized of the bunch. Flagship paid candidate.
- [ ] **Fleet hygiene (Intune / Autopilot / stale devices)** — cloud-managed cleanup. Pure MSP/paid territory.

---

## The workshop

Bigger builds — full apps, not single scripts. Different shape, same trust story: rule 4 gets rewritten (an app is an install, not a download-and-run `.ps1`), but low friction still means no runtime to chase and no account to create before it does something useful. Everything else holds.

### 🔨 In progress
- **LogHunter** (.NET) — a log viewer with AI on top. Open a gnarly log, and it surfaces the errors that actually matter and explains, in plain English, what broke. The pitch is Event Viewer's job done properly: the pain isn't reading one log line, it's finding it.

**Open questions** — worth settling before much code gets written:
- **Which logs?** Windows Event Log only, or flat files / IIS / app logs too? Event Log is the tightest story and the obvious pairing with the stash; flat files widen the audience a lot.
- **Where does the AI run?** Local model vs. hosted API changes the privacy pitch, the cost model, and the install size. Logs are sensitive by nature — "your logs stay on your machine" is a strong differentiator if it's affordable, and a rule 2 question either way.
- **Does it work with the AI off?** Recommend yes. If it's a decent viewer on its own, the AI is an assist rather than a dependency — and it degrades gracefully when the key's missing or the model's down.
- **Free or paid?** First real candidate for the paid lane that doesn't need a domain or tenant to test, which makes it a much easier thing to build and sell than the AD/M365 pack.

---

## Build order

1. ~~SquirrelCleaner~~ ✅
2. ~~Disk-Hog Finder~~ ✅
3. ~~Network Repair Kit~~ ✅
4. **LogHunter** 🔨 — first app, first thing in the workshop.

Three solid, safe, Reddit-friendly tools — none needing a domain to test — before touching anything else. That's done, and LogHunter is the next build: a bigger swing than a script, but still testable on one machine with no domain or tenant. The AD/M365 lane waits until the free stash has traction and there's a reason to build the paid module.

---

## Free vs paid, in one line

The free scripts are the lure — single tools that solve one painful thing and build trust. The paid module is the *curated, ready, supported* pack. The code was never the moat; the curation and the trust are. Lead every tool with the preview-first safety story and the brand reads as trustworthy on sight.

Apps sit somewhere else on that line: a script is a favour, an app is a product. LogHunter is the first test of whether the trust the stash earned carries over to something people install — and possibly pay for.

---

<sub>Part of [SquirrelScripts](https://squirrelscripts.github.io) · Built in a tree.</sub>
