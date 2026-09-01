# Week 1: Identity and Governance (Part 1) - Theory

**AZ-104 domain:** Manage Azure identities and governance (20-25%, highest priority)
**Objectives covered:** Manage Microsoft Entra users and groups, manage access to Azure resources

---

## 1. Microsoft Entra ID: the basics

Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's cloud identity and access management service. It is the directory that sits *above* Azure subscriptions, not inside them.

| Concept | What it is |
|---|---|
| Tenant | A dedicated, isolated instance of Entra ID. One organisation usually has one tenant. |
| Directory | Synonym for tenant in most contexts. |
| Subscription | A billing and scoping boundary for Azure resources. A tenant can contain many subscriptions. |

**Key relationship:** a subscription trusts exactly one Entra tenant for authentication, but a tenant can be trusted by many subscriptions. This is why Entra ID and Azure RBAC are described as two separate systems (see section 4).

### AWS comparison

If you know AWS IAM, the closest mapping is: Entra ID ~ the identity provider, Azure RBAC ~ IAM policies attached to resources. AWS bundles both into IAM; Azure splits them. There is no single Azure service that maps to a full AWS IAM policy document.

---

## 2. Users

### User types

| Type | Source | Typical use |
|---|---|---|
| Cloud-only | Created directly in Entra ID | Cloud-native orgs, this lab |
| Synced (hybrid) | Synced from on-prem AD via Entra Connect | Enterprises with existing AD |
| Guest (B2B) | Invited from another organisation or a personal Microsoft/Google account | External contractors, partners, cross-tenant collaboration |

### Guest users (B2B collaboration)

- Invited by email; they accept an invitation and authenticate with their *own* home tenant's credentials (or a Microsoft/Google account) - no separate password to manage on your side.
- A guest object is created in your tenant with `userType = Guest`, `usage location`, and a `UserPrincipalName` in the form `guestemail_domain.com#EXT#@yourtenant.onmicrosoft.com`.
- Default guest permissions are heavily restricted compared to members (governed by **External collaboration settings**). Guests can be granted more or less access via these settings.
- Access to resources (apps, RBAC roles, groups) still has to be assigned explicitly - inviting a guest does not by itself grant any resource access.

**Exam trap:** guest users are a *directory* concept (who can sign in), separate from RBAC role assignment (what they can do once signed in). An invited guest with no role assignment can sign in but sees nothing.

---

## 3. Groups

### Group types

| Type | Purpose |
|---|---|
| Security group | Used to grant access to resources (Azure RBAC, apps, file shares) |
| Microsoft 365 group | Collaboration group (shared mailbox, calendar, Teams, SharePoint) plus can also be used for access |

### Membership types

| Membership | How members are added | Licence requirement |
|---|---|---|
| Assigned | Manually added/removed by an admin | None |
| Dynamic user | Rule evaluated against user attributes (department, job title, etc.) | Entra ID P1 |
| Dynamic device | Rule evaluated against device attributes | Entra ID P1 |

Dynamic membership rules use a query syntax, e.g.:

```
(user.department -eq "Engineering") -and (user.country -eq "SG")
```

Membership is re-evaluated automatically whenever a matching attribute changes - no manual maintenance once the rule is right.

**Exam trap:** dynamic membership requires Entra ID P1 or P2. If a scenario says "the organisation has Free/Office 365 apps only tier" and asks how to automate group membership, dynamic groups is not a valid answer.

### Group-based licensing

Licences (e.g. Microsoft 365, Entra ID P1/P2) can be assigned directly to a user or to a group. Group-based licensing means every member of the group inherits the licence automatically - the standard pattern at scale, since assigning licences one user at a time does not survive org growth.

---

## 4. Azure RBAC vs Entra roles - the split system

This is the single most tested conceptual trap in the identity domain.

| | Azure RBAC | Entra roles |
|---|---|---|
| Controls | Access to **Azure resources** (VMs, storage, networking, subscriptions...) | Access to the **directory** itself (users, groups, app registrations, licences, tenant-wide settings) |
| Scope levels | Management group, subscription, resource group, resource | Tenant-wide (some roles can be scoped to an administrative unit) |
| Example roles | Owner, Contributor, Reader, Virtual Machine Contributor | Global Administrator, User Administrator, Helpdesk Administrator |
| Assigned via | Access control (IAM) blade on a resource/RG/subscription/management group | Entra ID > Roles and administrators |

**Being Owner of a subscription does not make you a Global Administrator, and vice versa.** A Global Administrator has no automatic access to Azure resources - though a Global Administrator can *elevate themselves* to gain User Access Administrator at root scope via a one-way toggle in Entra ID Properties, which is itself a testable fact (this is the documented bridge between the two systems, and it is deliberately not automatic).

---

## 5. Azure RBAC fundamentals

### The three parts of a role assignment

1. **Security principal** - who: a user, group, service principal, or managed identity.
2. **Role definition** - what: a collection of permissions (e.g. `Microsoft.Compute/virtualMachines/start/action`).
3. **Scope** - where: the boundary the permissions apply to.

### Scope hierarchy (permissions inherit downward)

```
Management group
   Subscription
      Resource group
         Resource
```

Assign a role at a higher scope and it applies to everything beneath it. Assigning **Reader** at the subscription gives read access to every resource group and resource inside that subscription, unless something more specific overrides it (Azure RBAC is additive-only - there is no explicit "deny" like AWS IAM has, only Deny assignments in very specific scenarios like Azure Blueprints/Blueprints locks, which are out of scope here).

### Key built-in roles

| Role | Grants |
|---|---|
| Owner | Full access, including managing access for others |
| Contributor | Full access to manage resources, but cannot grant access to others |
| Reader | View everything, change nothing |
| User Access Administrator | Manage user access to Azure resources only (no resource management) |

### Checking effective access

The IAM blade has a **"Check access"** feature: pick a user/group/service principal and it shows every role assignment that applies to them at that scope, aggregated from all the scopes above it. This is the practical tool for answering "why can/can't this person do X" - and the exam likes to test whether you can reason through inherited assignments without the tool.

**Exam trap recap:**
- Azure RBAC vs Entra roles are two separate systems with separate role stores and separate blades.
- Role assignments are additive and inherit downward only (never upward, never sideways).
- Owner can grant/revoke access to others; Contributor cannot.

---

## 6. Self-service password reset (SSPR)

SSPR lets users reset their own password without calling IT, using pre-registered authentication methods (phone, email, authenticator app, security questions).

- Requires a licence tier that supports SSPR (Entra ID Free has combined registration but limited SSPR scope; P1/P2 unlocks full SSPR for all users).
- Configured under **Entra ID > Password reset**.
- Can be scoped to: none, selected users/groups, or all users.
- Requires a minimum number of authentication methods (commonly 2) before a reset is allowed, configurable per policy.
- Combined registration ties MFA and SSPR method registration into a single user-facing setup experience.

**Exam trap:** SSPR is a self-service *user* capability. It is unrelated to an admin resetting someone else's password from the portal, which is a separate action under Entra ID > Users and does not depend on SSPR being enabled at all.

---

## 7. What to be able to do from memory before moving to labs

- Explain the difference between a cloud-only user, a synced user, and a guest user.
- Explain assigned vs dynamic group membership, and state the licence requirement for dynamic.
- State, without hesitating, that Azure RBAC and Entra roles are separate systems.
- Name the four Azure RBAC scope levels in order and explain that permissions inherit downward.
- Explain the difference between Owner and Contributor in one sentence.
- Explain what SSPR does and where it is configured.
