---
layout: post
title: What Happens When We Can No Longer Trust a Security Control?
date: 2026-09-18 00:00:00 +0530
description: What a compromised security control reveals about architectural trust,
  shared dependencies, and defense in depth.
categories:
- OT-Cybersecurity
- Security-Architecture
---

During one of my OT cybersecurity training sessions, a participant asked a question that made me rethink how we often explain defense in depth.

“Most security solutions are deployed around the higher levels of the architecture. Level 1 is several levels below. What happens if an attacker compromises one of those security solutions first and then uses it to move deeper without being detected?”
It is a simple question, but it exposes an important architectural challenge.

The question isn't necessarily whether security solutions are weaker than PLCs, RTUs, HMIs or other OT assets.

In many environments, they are actually better protected.

The more interesting question is:

What capabilities does an attacker gain when a trusted security control is compromised?
That changes the conversation from “Is the security product secure?” to:

“What happens to the architecture when we can no longer trust it?”

## Purdue is useful, but it isn't the complete security architecture
The Purdue Model is extremely useful for understanding the functional hierarchy of an industrial environment:

Enterprise → Site Operations → Operations Management → Supervisory Control → Basic Control → Process

But the Purdue Model alone doesn't tell us:

- Which assets can communicate
- Which communication paths are permitted
- Which identities are trusted
- Where privileged access exists
- Which systems can administer other systems
- What happens if a security control is compromised

This is where a security architecture based on concepts such as IEC 62443 zones and conduits becomes important.

Purdue helps us understand where systems function.

It doesn't, by itself, define how trust and communication should be controlled between them.

## Security solutions are assets too
Consider the technologies we commonly deploy around OT:

Firewalls | VPN gateways | Jump servers | PAM | IDS/NDR | SIEM | OT monitoring

These systems can have stronger security capabilities than many legacy OT assets:

- MFA
- RBAC
- Secure management protocols
- Hardening
- Regular patching
- Configuration backups
- Privileged-access controls

And because they generally aren't directly responsible for deterministic process control, there can be more flexibility to apply restrictive security controls.

So I wouldn't argue that:

“Security solutions are easy targets.”
The better argument is:

“Security solutions are high-value assets because of what they can see, control, authenticate or provide access to.”
A firewall knows something about network policy.

A jump server provides a controlled path into another environment.

PAM manages privileged identities.

An IDS/NDR provides visibility.

A SIEM aggregates security evidence.

An OT monitoring platform can provide detailed knowledge about assets and communications.

Their value to defenders can also make them valuable to attackers.

## Follow the capability, not the box
This is where the participant's question becomes particularly interesting.

It is tempting to draw an attack path like:

Attacker → Firewall → Level 3 → Level 2 → Level 1 → PLC

But compromising a firewall does not automatically give an attacker control of a PLC.

Instead, we should ask:

What capabilities does the compromised asset provide?
Access

↓

Trust

↓

Privilege

↓

Connectivity

↓

Capability

↓

Process impact

For example:

- What systems can it access?
- Which networks can it communicate with?
- What identities or credentials does it hold?
- What privileges does it have?
- Which systems trust it?
- Can it modify traffic or configuration?
- Can it provide a legitimate remote-access path?
- Can those capabilities ultimately affect the process?

This produces a much more meaningful attack path than simply following the boxes on a Purdue diagram.

## Remote access deserves special attention
This becomes particularly relevant with remote-access infrastructure.

Jump servers, VPN gateways and remote-access platforms exist precisely because they provide connectivity into environments that would otherwise be isolated.

That makes them operationally useful.

It also makes them important security boundaries.

MITRE ATT&CK for ICS identifies External Remote Services (T0822) as a technique for gaining access to control-system environments and specifically discusses remote-access mechanisms such as VPNs and jump hosts.

So the question shouldn't simply be:

“Do we have a VPN?”
It should be:

When is remote access enabled?

Who can use it?

What can that identity reach?

What can the session do?

Is access persistent or time-bound?

Is the session monitored?

What happens if the remote-access infrastructure itself is compromised?

These questions are especially important for third-party and vendor access.

## We have seen the consequences of compromising trusted protective systems
The TRITON/TRISIS incident provides an important OT lesson.

TRITON targeted Schneider Electric Triconex safety instrumented systems at a refinery. CISA reported that the incident resulted in an unplanned shutdown of the facility.

An SIS isn't a cybersecurity control in the conventional sense.

But the incident demonstrates a broader principle:

Systems that occupy a trusted and protective position in an industrial environment can themselves become high-value targets.
The same principle should influence how we think about security infrastructure.

## The hidden problem: security dependencies
Now consider an architecture with:

Firewall + PAM + Jump Server + IDS/NDR + SIEM + OT Monitoring

On a diagram, this looks like multiple layers of defence.

But how independent are they?

What if:

- PAM depends on Active Directory
- The jump server uses the same identity infrastructure
- Security appliances are administered through the jump server
- Monitoring depends on the same network infrastructure
- Logs from multiple controls go to the same SIEM
- Several systems share the same privileged administrators

An attacker may not need to defeat every security product individually.

They may only need to compromise a common dependency.

This is why defence in depth shouldn't be measured simply by the number of security products deployed.

We also need to understand their:

dependencies, trust relationships and failure modes.

## What should we do differently?
The discussion becomes much more useful when it leads to architectural actions.

### 1. Treat security infrastructure as critical assets

Include firewalls, VPN gateways, jump servers, PAM, monitoring infrastructure and security-management systems in the asset inventory and threat model.

### 2. Use risk-driven segmentation

Use the Purdue Model to understand the functional hierarchy, but use a risk-based approach such as IEC 62443 zones and conduits to determine security boundaries and permitted communication.

### 3. Minimize standing privilege

Use strong authentication, least privilege and, where operationally practical:

- Just-in-time access
- Time-bound vendor access
- Separate administrative accounts
- Session monitoring
- Controlled remote-access paths

### 4. Don't make one system your only source of truth

If security monitoring, logging and management all depend on the same infrastructure, a single compromise can affect both the attack and our ability to see it.

Independent monitoring and protected log storage can reduce this dependency.

### 5. Design for security-control failure

For every important control, ask:

“What happens if this control is disabled, bypassed, fails open, fails closed, or is fully compromised?”
The answer should be part of the architecture.

### 6. Identify the real crown jewels

The ultimate target may not be the firewall.

It may be:

Engineering workstation → PLC

SCADA server → control function

Safety engineering environment → SIS

The architecture should therefore focus on protecting the systems and functions whose compromise could create meaningful operational or safety impact.

## The question I would now ask in an architecture review
Instead of asking only:

“Do we have enough security controls?”
I'd ask:

“Which security controls does the architecture trust, what do they trust in turn, and what happens if one of them is compromised?”
Then follow the attack path:

Access → Trust → Privilege → Connectivity → Capability → Impact

That exercise can reveal dependencies and attack paths that aren't obvious from a Purdue diagram.

## The takeaway
The participant's question wasn't really about whether firewalls, IDS or jump servers are secure enough.

It was about architectural trust.

A security control can be well hardened and still be compromised.

A remote-access system can have MFA and still become an attack path.

A monitoring system can provide excellent visibility and still become a blind spot if its dependencies are compromised.

And a Purdue diagram can show us where systems function without telling us everything about how an attacker can move between them.

Defense in depth is not simply “more security products.”

It is an architecture in which:

- Critical assets are identified
- Zones and conduits are risk-driven
- Privileges are minimized
- Remote access is tightly controlled
- Security dependencies are understood
- Detection doesn't depend entirely on one component
- And the compromise of one control doesn't automatically collapse the rest of the defensive architecture

So perhaps the most useful question from that training session is not:

“What if the attacker compromises the security solution?”
It is:

“What happens to our architecture when we can no longer trust one of our security controls?”
That is where defense in depth stops being a diagram and becomes an engineering problem.
