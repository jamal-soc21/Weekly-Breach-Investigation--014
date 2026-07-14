# Weekly-Breach-Investigation--014

Weekly Breach Investigation
Breach: CrashStealer — macOS Information Stealer
Analyst: Jamal Mahmoad
Date: 2026-07-14

Summary
CrashStealer is a newly discovered macOS stealer written in C++ and distributed through a signed, notarized dropper (Werkbit.app). Unlike commodity stealers, it bypasses Gatekeeper checks and uses a careful delivery chain involving domains, GitHub repos, and staged payloads. Once executed, it validates the user’s password locally, unlocks the keychain, and collects sensitive data from browsers, cryptocurrency wallets, password managers, and personal directories. The stolen data is encrypted with AES‑GCM and exfiltrated to attacker infrastructure.

Attack Flow
Distribution via werkbit[.]io with a notarized disk image.

Dropper fetches payload from GitHub (mgothiclove/sys.cache).

Persistence through LaunchAgent.

Password validation → keychain unlocked.

Harvests credentials, wallets, password managers, and files.

Data encrypted and sent to 179.43.166[.]242.

Mitigation
Block suspicious notarized apps and monitor Gatekeeper bypass attempts.

Watch for LaunchAgent persistence entries.

Detect unusual AES‑GCM encrypted traffic.

Track related domains and GitHub infrastructure.

Analyst Notes
CrashStealer shows a professional design with encryption, obfuscation, and anti‑analysis techniques. Its notarized delivery chain makes detection harder, and evidence suggests it is part of a larger multi‑platform campaign targeting multiple ecosystems
