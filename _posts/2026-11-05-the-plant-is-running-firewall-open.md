---
layout: post
title: "The Plant Is Running. The Firewall Is Open. Who Owns the Risk?"
date: 2026-11-05 00:00:00 +0530
description: "The overlooked reality of OT firewall commissioning, security competency, and long-term ownership."
categories: [OT-Cybersecurity, Firewalls]
---

*The overlooked reality of OT firewall commissioning, security competency, and long-term ownership.*

In many OT environments, firewalls are installed, VLANs are configured, and network segmentation looks perfectly reasonable on architecture diagrams. Yet, when we examine the actual firewall policies, we sometimes find overly permissive rules, including *any-any*.

For cybersecurity professionals, this can be frustrating. But before questioning why someone configured the firewall this way, perhaps we should understand the reality of OT commissioning.

## The Commissioning Reality

**Who actually commissions an industrial automation system?**

In many projects, it is the Automation Engineer, already responsible for PLC programming, SCADA configuration, loop checks, logic verification, field integration, and troubleshooting. Their primary objective is to make the plant operational within the project schedule.

On top of these responsibilities, they may also be expected to configure managed switches, VLANs, routing, and industrial firewalls.

In a relatively flat network, communication is often straightforward. Introduce VLANs and firewall-based segmentation, and things become more complicated. Suddenly, SCADA cannot communicate with controllers, engineering stations cannot discover PLCs, or certain services stop working.

The engineer now has to troubleshoot routing, firewall policies, and industrial protocol requirements while the commissioning deadline approaches.

**What's the easiest way out when firewall filtering is the problem?**

Configure an *any-any* rule. Communication is restored. Functional testing passes. Commissioning moves forward.

**But what happened to the original intent behind segmentation?**

## The Problem Doesn't End at Commissioning

There is nothing inherently wrong with temporarily allowing broader communication for controlled troubleshooting.

> **The problem begins when temporary configurations become permanent.**

The VLANs still exist. The firewall is physically present. The architecture diagram continues to show separate security zones. But the intended communication restrictions may no longer be effectively enforced.

Now consider what happens after commissioning.

The system integrator hands over the plant, the commissioning engineers move to another project, and the firewall becomes part of the operational infrastructure.

**Who maintains it?**

Who reviews firewall policies after handover? Are security-relevant logs collected and monitored? Who investigates suspicious communication attempts? When equipment or communication requirements change, who ensures firewall policies are updated accordingly?

If we struggled to establish the necessary security expertise and validation during commissioning, what arrangements ensure those capabilities are available throughout the plant's operational life?

A firewall configured once and forgotten is not a sustainable security control.

## Are We Addressing the Real Problem?

We specify network segmentation, procure industrial firewalls, and reference cybersecurity standards. But are we ensuring the **competency, validation, and operational ownership** necessary to make those controls effective?

We cannot expect every Automation Engineer to become a cybersecurity specialist overnight. Equally, cybersecurity professionals cannot simply provide architecture diagrams and expect commissioning teams to figure out the implementation.

Security expertise must be available during engineering and commissioning. Automation engineers and vendors should establish communication requirements, while network and cybersecurity specialists translate them into enforceable policies.

Commissioning should verify both that **required communication is permitted and prohibited communication is blocked**. Operational maintenance must then ensure those restrictions remain effective as the system evolves.

Beyond handover, someone must own policy maintenance, rule reviews, security monitoring, and change management.

**Security cannot end with successful commissioning. It must remain effective throughout the system's operational lifecycle.**

## The Bigger Question

Perhaps the issue isn't simply why an Automation Engineer configured an *any-any* rule.

It is why our project execution approach made that the easiest solution, why validation didn't identify it as an unresolved security concern, and whether anyone will revisit it once the plant is operational.

A firewall being installed is not the same as a firewall providing security.

> **OT cybersecurity is not just about deploying the right controls. It is about having the competency to implement them, the discipline to validate them, and the ownership to maintain them.**

---

**In your OT projects, who takes ownership of firewall policies, monitoring, and security validation after the commissioning team leaves?**