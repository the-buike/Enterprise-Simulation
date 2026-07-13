# Ashgrove Regional Medical Center: Healthcare IT Infrastructure Project (Planned)

![Project banner](./images/project-banner.png)

A planned expansion of the home lab into a fictional hospital network: a public-facing hospital website paired with a fully segmented internal network, Active Directory-based identity management, and department-level access control modeled on real healthcare IT practices.

---

## Concept

Rather than a generic fictional company, this project is framed as **Ashgrove Regional Medical Center**, a fictional hospital. Healthcare IT has some of the clearest, most well-documented real-world requirements for network segmentation and access control (driven by HIPAA), which makes it a stronger, more realistic training ground than an arbitrary business.

- **Public domain (planned):** `ashgroveregional.org`
- **Internal AD domain (planned):** `ad.ashgroveregional.org`
- **NetBIOS name (planned):** `ASHGROVE`

This follows the same split-brain DNS pattern documented in the [Active Directory knowledge base](./active-directory-kb.md): the public domain resolves externally to the hospital's website, while the internal AD zone resolves only for devices inside the network and is entirely unreachable from the public internet.

---

## Planned Department / OU Structure

| OU | Represents |
|---|---|
| Administration | Hospital administrative staff |
| Nursing | Nursing staff |
| Radiology | Imaging department |
| Laboratory | Lab staff |
| Emergency Department | ED staff |
| IT | IT/systems administration |
| Human Resources | HR staff |

---

## Planned Access Control Model

This is the centerpiece of the project, department-based security groups enforcing real access boundaries on a shared file server:

| Security Group | Access |
|---|---|
| `Radiology-ReadWrite` | Full access to an imaging file share |
| `HR-Confidential` | Restricted access to an HR share, deliberately excluding IT admins by default, demonstrating least-privilege access even for administrators |
| `AllStaff-ReadOnly` | Read-only access to a hospital-wide announcements share, used as a contrast case against the restricted shares above |

Verification will include screenshots of both a granted-access case and a denied-access case, using two distinct test users so the access control is demonstrably working, not just configured.

---

## Relationship to the Existing Home Lab

This project builds directly on infrastructure already in place:

- **Networking:** the existing MikroTik VLAN structure (see [`network-infrastructure-kb.md`](./network-infrastructure-kb.md)) provides the segmentation model; a DMZ VLAN is a natural fit for the hospital's public-facing website
- **Active Directory:** the existing `homelab.local` forest (see [`active-directory-kb.md`](./active-directory-kb.md)) can either be extended or rebuilt under the new domain naming, this decision is still open
- **Documentation approach:** this project will follow the same style as the existing docs, architecture and decisions first, troubleshooting called out explicitly, screenshots used selectively to prove function rather than illustrate every step

---

## Status

**Planning stage.** No components of this specific project have been built yet. See [`fictional-company-project-kb.md`](./fictional-company-project-kb.md) for the original concept notes this project is based on. This README will be updated as work begins, and a dedicated knowledge base document will be built out alongside the actual implementation.
