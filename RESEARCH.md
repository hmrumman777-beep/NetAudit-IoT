# Deep Analysis: UPnP Vulnerabilities in SOHO Routers
**Target:** TP-Link Archer C20 (libupnp 1.6.19)

## Architecture Analysis
The **TP-Link Archer C20** utilizes the **Portable SDK for UPnP (libupnp) version 1.6.19**. This legacy SDK is compiled into the router's firmware (MIPS architecture) and runs as an unauthenticated service on port 1900.

## Critical Vulnerability: CVE-2012-5958
- **Type:** Stack-based Buffer Overflow.
- **Root Cause:** Insecure handling of `unique service name` (USN) headers in SSDP (Simple Service Discovery Protocol) replies.
- **Exploitation:** By sending a specially crafted UDP/TCP packet with an overlong USN string, an attacker can overwrite the return address on the stack.
- **Impact:** Remote Code Execution (RCE) with root privileges on the router.

## Proof of Concept (Manual Audit)
1. **Discovery:** Identifed open port 1900/TCP.
2. **Fingerprinting:** Captured server banner: `Portable SDK for UPnP devices/1.6.19`.
3. **Fuzzing:** Attempted to map SOAP control points via `/rootDesc.xml`.

## Remediation
- **For Users:** Disable UPnP via the web interface (`Advanced > NAT Forwarding`).
- **For Developers:** Recompile firmware with `libupnp 1.14.12+` which includes patches for memory corruption bugs.