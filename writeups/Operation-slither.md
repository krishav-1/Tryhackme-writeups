# TryHackMe — Operation Slither

**Platform:** [TryHackMe](https://tryhackme.com)  
**Difficulty:** Easy  
**Category:** OSINT (Open-Source Intelligence)  
**Status:** ✅ Completed

---

## Overview

A digital investigation challenge simulating the tracking of a cybercriminal group ("Sneaky Viper") responsible for breaching a fictional telecom company and leaking customer data. Starting from a single forum post and username, the goal was to identify three group members by pivoting across social media platforms and uncovering hidden flags along the way — entirely through OSINT, with no exploitation involved.

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Google Search | Cross-platform username pivoting |
| X / Twitter | Initial lead on the group leader |
| Threads | Tracing conversations between operators |
| Instagram | Identifying the second operator's profile |
| SoundCloud | Finding hidden encoded messages in track descriptions |
| GitHub | Investigating commit history for leaked information |
| CyberChef | Decoding Base64-encoded flags |

---

## Methodology

### Step 1 — Identifying the Leader

Started with a forum post where a user (`v3n0mbyt3_`) claimed responsibility for the breach. Searched the handle across platforms and found a matching account on Threads. Reading through their posts and replies led to the first flag, hidden in a thread reply.

This also revealed a second username interacting with the leader: `_myst1cv1x3n_`.

---

### Step 2 — Finding the Second Operator

Searched `_myst1cv1x3n_` and found an Instagram profile linking out to a SoundCloud account. On SoundCloud, the description of a track called "Prototype2" contained a Base64-encoded string.

Decoded it using CyberChef's **From Base64** recipe to reveal the second flag.

---

### Step 3 — Finding the Third Operator

The same SoundCloud track included audio referencing GitHub repos and tooling. Checking the account's followers/interactions surfaced a third handle: `sh4d0wF4NG`.

Searched this handle and found a GitHub profile with public repositories matching a phishing toolkit advertised in a separate forum post (Terraform scripts, phishing infrastructure, etc.).

Reviewed the commit history of the `red-team-infra` repository — commit diffs contained the information needed to retrieve the third and final flag.

---

## Flags

> **Flag 1:** `THM{REDACTED}`  
> **Flag 2:** `THM{REDACTED}`  
> **Flag 3:** `THM{REDACTED}`

---

## Key Takeaways

- **Cross-platform pivoting** is one of the most effective OSINT techniques — reused usernames link accounts together even when operators try to compartmentalize
- **Network mapping** (followers/following/replies) reveals associates that aren't directly advertised
- **Git forensics** matters — developers often leak sensitive details in commit history that isn't visible in the current state of a repo
- Real threat actors get caught the same way: small OPSEC mistakes compound into full identification
- This room reinforced skills directly relevant to **SOC and threat intelligence work** — correlating fragmented data points into a complete picture

---

## References

- [TryHackMe — Operation Slither](https://tryhackme.com/room/operationslitherIU)
- [CyberChef](https://gchq.github.io/CyberChef/)
