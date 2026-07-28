<div align="center">

# Veil

**Find out what your machine is telling everyone. Then stop it.**

[![version](https://img.shields.io/badge/version-0.2.0-8b5cf6)](https://github.com/BiksY01/veil/releases)
[![platforms](https://img.shields.io/badge/platforms-Linux%20%7C%20Windows-8b5cf6)](#what-runs-where)
[![no telemetry](https://img.shields.io/badge/telemetry-none-6ee7b7)](#what-veil-does-not-do)
[![offline licence](https://img.shields.io/badge/licence%20check-offline-6ee7b7)](#free-and-plus)

</div>

Veil reads your machine's actual privacy posture — DNS, VPN tunnel, traffic egress,
firewall, IPv6 leaks, MAC randomisation, encrypted messaging, disk encryption — and
tells you plainly which of them are open. For every gap it shows the exact commands
for *your* distribution, and what each one does not fix.

It is closed source. This repository is the download page, the changelog and the
issue tracker — the source lives elsewhere.

---

## How it works

```
scan  →  review  →  preview  →  apply  →  revert
```

1. **Scan.** Eight read-only checks. Nothing is changed and nothing leaves the machine.
2. **Review.** Each result says what it means, why it matters, and what it does not cover.
3. **Preview.** Before anything runs you see the exact paths, services and values that
   would change. No fix is ever applied without you reading it first.
4. **Apply.** Through a small helper that validates every request against a fixed
   allowlist. The interface itself never runs with elevated privileges.
5. **Revert.** Every fix has an undo. Veil can also write out a commented
   revert-everything script you can read before running.

## What runs where

Declared in [`support-matrix.json`](support-matrix.json), which the app, this page and
the website all read. If they ever disagree, that file is right.

| Check | Linux | Windows |
|---|:--:|:--:|
| Encrypted DNS | ● | ● |
| VPN tunnel | ● | ● |
| Traffic egress | ● | ● |
| Firewall default-deny | ● | ● |
| IPv6 leak guard | ● | ● |
| MAC randomisation | ● | ◐ |
| Encrypted messaging | ● | ● |
| Disk encryption | ● | ● |

● full · ◐ narrower answer than on Linux, and the app says so

**Linux is first-class.** systemd, OpenRC, runit, s6, dinit and SysV init are all
detected rather than assumed, across apt, dnf, pacman, portage, zypper, apk, xbps and
nix. If Veil cannot identify your init system or package manager, it tells you what to
do in plain English instead of guessing a command — a wrong command run as root is
worse than no command.

**Windows is in development.** No download yet. It is listed here because it is being
built, not to pad the table.

**macOS and Android are not supported and are not planned.** macOS cannot be built or
signed without Apple hardware and a paid developer account. On an unrooted Android,
firewall state, IPv6 routing and the Wi-Fi MAC are simply not readable — which is most
of what Veil does. Shipping either would mean shipping something that mostly says
"can't tell".

## Free and Plus

The free tier is the honest auditor: every check, the full score, and three fixes you
can apply. It is meant to be genuinely useful on its own.

| | Free | Plus — €18, once |
|---|:--:|:--:|
| All eight checks and the score | ● | ● |
| Why each gap matters, and its limits | ● | ● |
| Apply: encrypted DNS, MAC randomisation, messaging | ● | ● |
| Apply: VPN, egress, firewall, IPv6, disk | | ● |
| Hardening profiles | | ● |
| Scheduled scans and posture history | | ● |
| Config backup and portability | | ● |
| Lifetime updates | | ● |

One payment, no subscription. Paid in Monero, direct — no card processor, no account,
no name required.

**The licence check is offline.** It verifies a signature against a key built into the
app. There is no activation server, no phone-home and no hardware fingerprinting.
Veil could not check up on you if it wanted to. An expired or invalid licence never
locks you out of fixes you already applied, and never blocks revert.

## What Veil does not do

This section is here because a privacy tool that oversells itself is worse than no tool.

- **It does not make you anonymous.** It reduces what passive observers — your ISP,
  the network you are on, commercial trackers — can casually collect. Against someone
  specifically targeting you, it is not the right tool and will not pretend to be.
- **It does not protect a machine you are logged into.** Disk encryption protects a
  powered-off laptop. It does nothing while the screen is unlocked.
- **It does not remove malware,** and it cannot tell you whether something is already
  running on your machine.
- **It does not audit your VPN provider.** A tunnel moves your trust from your ISP to
  them. Veil confirms the tunnel is up and carrying traffic. Whether they deserve that
  trust is your call.
- **It does not change anything you have not read and agreed to.** No fix is applied
  silently and nothing persists across a reboot unless you switch that on per fix.
- **It does not collect anything.** No telemetry, no analytics, no crash reports, no
  unique identifier. Update checks fetch a signed manifest and send nothing.

## Download

Releases are on the [releases page](https://github.com/BiksY01/veil/releases), with a
`SHA256SUMS` file and a signature for every artifact.

```bash
# check what you downloaded before you run it
sha256sum -c SHA256SUMS --ignore-missing
```

Linux ships as an AppImage: one file, `chmod +x`, double-click. It offers to add a
desktop entry on first run and does nothing without being asked.

## Security

Found something? See [SECURITY.md](SECURITY.md). Please report privately first.

The privilege boundary is the part worth scrutinising: the interface never runs
elevated. A separate helper does, per action, against an allowlist derived from the
fix catalogue — it takes an opaque check id and maps it to a command from its own
fixed table, so nothing you type reaches a shell.

## Chat Control, accurately

The two proposals get conflated constantly, including by people reporting on them.

- **Chat Control 1.0** — the temporary derogation permitting *voluntary* scanning —
  lapsed on 3–4 April 2026 and was reinstated on 9 July 2026, when Parliament fell
  short of the 361-vote absolute majority needed to reject the Council's fast-tracked
  text. 314 voted to reject. Voluntary suspicionless scanning may continue until 2028.
- **Chat Control 2.0 (CSAR)** — the permanent regulation, with mandatory detection
  orders and possible client-side scanning — **is not law**. It remains in trilogue.
  The fifth and expected-final session on 29 June 2026 did not resolve it. Talks resume
  in September 2026.

Veil does not protect you from client-side scanning, and nothing can — that is the
point of it. What Veil covers is the layer below: what your machine leaks before any
of that applies.

*Last verified: 2026-07-28.*

## FAQ

**Is it open source?** No. The checks and what they do are documented in full, and the
fix commands are shown before they run, so you can verify every claim against your own
machine — but the source is not published.

**Why should I trust a closed-source privacy tool?** You should not, on faith. Veil
makes no network connections except the egress check, which you can watch. It applies
nothing without showing you the exact commands first. Run it behind a firewall log if
you want to confirm.

**Will it break my system?** Every fix shows a preview and has a revert. The riskiest
ones are flagged and ask twice. Disk encryption is deliberately advisory only — Veil
will never reformat anything.

**Does it work on my distro?** If it is Linux, probably. If Veil cannot identify your
package manager it degrades to instructions rather than guessing.

**I paid and switched machines.** The licence is not tied to hardware. Paste the same
key.
