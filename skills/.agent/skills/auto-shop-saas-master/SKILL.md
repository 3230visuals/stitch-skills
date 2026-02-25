---
name: auto-shop-saas-master
description: End-to-end build system for a multi-tenant auto repair SaaS with Owner, Staff, and Client portals, progress workflow, messaging, VIN lookup, QR invites, and Stripe Connect marketplace logic. Use when building or rebuilding the auto shop app in Antigravity.
---

# Auto Shop SaaS Master Skill

This skill defines how to properly build and scale the Auto Shop SaaS app in stages.

Follow the phases in order. Do not skip.

---

## PHASE ORDER (Always Follow This)

1. Routing first
2. Data structure second
3. Core workflow third
4. Invites fourth
5. Payments fifth
6. Animations last

Never add animations before routing works.

---

## PHASE 1 — ROUTING ONLY

Create all pages with empty content first.

### Required Routes

/app  
/app/owner  
/app/owner/jobs  
/app/owner/jobs/[jobId]  
/app/owner/staff  
/app/owner/clients  
/app/owner/invites  
/app/owner/payments  

/app/staff  
/app/staff/jobs  
/app/staff/jobs/[jobId]  

/app/client  
/app/client/jobs  
/app/client/jobs/[jobId]  

Success condition:
- Every page loads
- Navigation works
- No animations yet

---

## PHASE 2 — DATA STRUCTURE

Create these core objects:

Shop  
User (role: OWNER | STAFF | CLIENT)  
Vehicle  
Job  
Stage  
Message  
Invoice  
Invite  

Every object must include:
- id
- shopId (multi-tenant support)

---

## PHASE 3 — PROGRESS BAR ENGINE

Rules:

- Stages are ordered
- Owner and Staff can move stage forward AND backward
- Client sees progress but cannot change it
- Every stage change logs history

Progress must not break routing.

---

## PHASE 4 — MESSAGING

- One message thread per Job
- Owner, Staff, Client can message
- Messages sorted oldest to newest
- No animations affecting message input

---

## PHASE 5 — INVITES + QR

Owner can generate:
- Staff invite link
- Client invite link

Invite must:
- Contain shopId
- Contain secure token
- Expire

QR encodes invite link.

---

## PHASE 6 — STRIPE CONNECT

Requirements:

- Shop connects Stripe account
- Client pays invoice
- Platform takes percentage fee
- Payment confirmed via webhook before marking PAID

Never mark invoice paid before confirmation.

---

## PHASE 7 — ANIMATIONS

Rules:

- Animations must NOT control routing
- Animations must NOT block pointer events
- Routing must work if animations removed

Themes:
Client = car style
Staff = mechanic style
Success = checkered flag animation

---

## DEBUG RULES

If button not clickable:
- Check z-index
- Check pointer-events
- Check overlay elements

If route wrong:
- Check path spelling
- Check slug vs id mismatch

If progress not updating:
- Verify stage id exists
- Verify state update persists

---

## WHEN THIS SKILL IS USED

The agent must output:

1. Current phase
2. Files to create or edit
3. Routes involved
4. Data types needed
5. Acceptance test checklist