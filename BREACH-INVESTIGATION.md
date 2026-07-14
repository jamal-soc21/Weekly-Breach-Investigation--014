Weekly Breach Investigation
Breach: CrashStealer — macOS Information Stealer
Analyst: Jamal Mahmoad
Date: 2026-07-14

Summary
CrashStealer is a new macOS information stealer written in native C++ and distributed via a signed, notarized dropper (Werkbit.app).
It bypasses Gatekeeper checks and harvests data from browsers, cryptocurrency wallets, password managers, and the macOS keychain.

Attack Flow
Signed disk image from werkbit[.]io gated by meeting PIN.

Dropper (veltod) fetches payload from GitHub (mgothiclove/sys.cache).

Downloader stages CrashReporter.dmg in /tmp.

Persistence via LaunchAgent.

Local password validation → unlocks keychain.

Harvests browser credentials, wallet extensions, password manager data, and files from ~/Documents and ~/Downloads.

Data encrypted with AES‑GCM and exfiltrated to 179.43.166[.]242.

 MITRE ATT&CK
Persistence: LaunchAgent (T1547)

Credential Access: Keychain Credential Theft (T1555)

Collection: Browser/Wallet/Password Manager Data (T1119)

Exfiltration: Encrypted Data Transfer via libcurl (T1041)

Mitigation
Block downloads from suspicious notarized apps (Werkbit.app).

Monitor LaunchAgent persistence entries.

Detect AES‑GCM encrypted outbound traffic.

Track domains and GitHub repos tied to mgothiclove.

Analyst Notes
CrashStealer stands out for its signed and notarized delivery chain, making it harder to detect.
Its use of AES‑GCM client‑side encryption, anti‑debugging, and obfuscation shows a highly professional build compared to commodity stealers.
Evidence suggests it is part of a larger multi‑platform campaign beyond macOS
