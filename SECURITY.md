# Reporting a security issue

Please report privately first, at **security@** the project's domain. Do not open a
public issue for anything exploitable.

Tell me what you found, how to reproduce it, and what you were able to achieve. A
proof of concept is welcome. I will confirm receipt within 72 hours and tell you
plainly whether I think it is a problem and what I intend to do.

No bounty — this is one person's project and pretending otherwise would be dishonest.
Credit in the release notes if you want it, and silence if you would rather.

## What I consider serious

Roughly in order:

1. **Privilege escalation through the helper.** It is the only component that runs
   elevated. It accepts an opaque check id and maps it to a command from its own fixed
   table — no argument, path or JSON field from the interface ever reaches a command
   line. If you can get it to run something outside that table, that is the highest
   severity issue in the product.
2. **A fix that damages a system,** or a revert that does not actually revert.
3. **Anything that makes Veil send data anywhere.** It has no telemetry by design; a
   path that leaks even a machine identifier contradicts the entire premise.
4. **A false "you are protected"** where the machine is not. Reporting safety that
   does not exist is worse than reporting nothing, because people act on it.
5. **Licence forgery.** Real, but honestly the least of these — it costs money, not
   safety.

## What is already known and accepted

Saying so up front to save you the time:

- **The licence check can be defeated by someone determined.** It is an offline
  signature check in a binary on your own machine. Anything stronger would mean phoning
  home, which would contradict the product. This is a deliberate trade.
- **Veil cannot verify a VPN provider's behaviour.** It confirms a tunnel exists and
  carries traffic. What happens at the other end is outside what any local tool can see.
- **A loopback resolver is trusted without auditing it.** If DNS points at 127.0.0.1,
  Veil assumes something local is doing the encryption rather than trying to verify
  that proxy's configuration and health.
- **Probe failure reports as "unknown", not as a failure.** This is intentional. A
  missing tool or a permission error is not evidence that a protection is absent.

## Scope

In scope: the application, the helper, the licence verification, the update mechanism,
the website and its build pipeline.

Out of scope: anything requiring physical access to an unlocked machine, social
engineering, and denial of service against the website.
