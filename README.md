# veil

linux anti-surveillance, for people who can't or won't do it by hand.

veil reads what's actually protecting your machine, tells you in plain words what's exposed
and why it matters, and — with your permission — fixes it. no terminal, no guides, no guessing.

> **status:** in development. not released yet. source is closed for now — this repo is just
> where i talk about it.

## what it does

it runs a set of honest, read-only checks and scores your posture:

- **encrypted dns** — stop your isp reading every site you visit
- **vpn tunnel + real egress** — confirm your traffic actually leaves encrypted, not just "connected"
- **kill-switch firewall** — no leak if the tunnel drops
- **ipv6 leak guard** — the leak most setups miss
- **mac randomization** — stop networks fingerprinting your device
- **encrypted messaging** — move private chats off apps that read them
- **disk encryption** — the gap that matters if the machine is ever taken

every gap explains itself: why it's bad, how to fix it, and the exact commands **for your
system** — because it detects your init (systemd / openrc / runit / …) and package manager,
so it never runs something that breaks your box. deep fixes ask before they touch anything.

## what it is not

i won't lie in an app whose whole point is not lying to you:

- it defeats your **isp and mass/passive surveillance**.
- it is **not anonymity**, and it will **not** hide you from someone specifically targeting you.
- no client app is "unhackable" or "undetectable" — anyone selling you that is scamming you.

veil makes you a hard target for everything short of that, and says so, everywhere.

## how it's built

- tiny **python (stdlib only)** backend — no dependencies, runs anywhere
- a plain **html/css/js** frontend — mono dark + light, real interactive 3d (a live "cyber
  network" view of your posture, a globe with your exit marked), no framework, no build step
- local-only + locked down: binds to localhost, strict content-security-policy, no telemetry

## tiers

- **free** — open tools anyone can use: cloudflare warp, dnscrypt, nftables
- **plus** — a later paid layer. no pricing decided, no fake paywall.

## roadmap

- one-click apply (consent-gated, via a small privileged helper)
- windows + mobile (their own detection backends — the linux probes don't translate)

---

built by [biksy](https://github.com/BiksY01) · more at [lukasz-aep.pages.dev](https://lukasz-aep.pages.dev)
