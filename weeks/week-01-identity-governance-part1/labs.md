# Week 1: Identity and Governance (Part 1) - Hands-on Labs

**Prerequisite:** an Azure free account (or pay-as-you-go) with Entra ID access. All labs in this file are free - no billable resources are created, only directory objects and role assignments. No cleanup budget risk this week.

**Method:** do every lab in the **Azure portal** first (this is what the exam tests - blade names and hotspot screens). Optionally repeat in CLI afterwards for muscle memory; CLI snippets are included at the end of each lab as a bonus, not a requirement.

Log your results directly in this file as you go - the `Notes` line under each lab is there for that. Do not skip writing them; the friction of typing what you observed is most of the learning value.

---

## Lab 1: Create users

**Goal:** create cloud-only users and understand the account lifecycle.

1. Go to **Entra ID > Users > New user > Create new user**.
2. Create at least 2 users, e.g. `alice-test` and `bob-test`, with auto-generated passwords.
3. Fill in optional properties for one of them: job title, department, usage location (required later for licensing).
4. Open one user's profile and explore the tabs: **Assigned roles**, **Assigned licenses**, **Groups**, **Sign-in logs**.
5. Try **Reset password** from the admin side on one user - note this is completely independent of SSPR (Lab 4).
6. Try **Block sign-in** on the other user, then unblock it. Note where this toggle lives.

**Notes:**
- [ ] Where does "usage location" matter later? _______________
- [ ] What's the difference between deleting a user and blocking sign-in? _______________

**CLI equivalent (bonus):**
```bash
az ad user create --display-name "Alice Test" \
  --password "ChangeMe123!ChangeMe" \
  --user-principal-name alice-test@<yourtenant>.onmicrosoft.com
```

---

## Lab 2: Create groups (assigned and dynamic)

**Goal:** compare the two membership models directly.

### Part A: assigned membership

1. **Entra ID > Groups > New group**.
2. Group type: **Security**. Membership type: **Assigned**.
3. Name it `sg-assigned-test`. Add `alice-test` and `bob-test` as members manually.

### Part B: dynamic membership

> Requires Entra ID P1 - the Azure free trial tenant includes a P1/P2 trial by default, so this should work. If your tenant does not have P1/P2 available, document that limitation instead of skipping the concept.

4. Create a second group `sg-dynamic-test`. Membership type: **Dynamic User**.
5. Add a dynamic membership rule, e.g.:
   ```
   (user.department -eq "Engineering")
   ```
6. Go set `alice-test`'s department to "Engineering" (Entra ID > Users > Alice > Properties > Job info).
7. Return to `sg-dynamic-test > Members` and watch (it can take a few minutes) for Alice to appear automatically.

**Notes:**
- [ ] How long did dynamic re-evaluation take? _______________
- [ ] What happens if you manually try to add a member to a dynamic group? _______________

**CLI equivalent (bonus):**
```bash
az ad group create --display-name "sg-assigned-test" --mail-nickname "sgassignedtest"
```
(Dynamic membership rules are portal/Graph-only for practical purposes - not worth scripting for this lab.)

---

## Lab 3: License assignment (group-based)

**Goal:** understand group-based licensing, even without a paid M365 licence available.

1. **Entra ID > Licenses > All products** - see what's available in your tenant (a free/trial tenant usually has an Entra ID P1 or similar trial SKU).
2. If any licence SKU is available: **Entra ID > Groups > sg-assigned-test > Licenses > Assignments**, assign a licence to the group and confirm both members inherit it.
3. If no licence SKU is available in your tenant, skip the assignment step but read the **Licenses > All products** blade and note what a real assignment flow would look like: group > Licenses > Assign.

**Notes:**
- [ ] What licence SKUs are visible in your tenant? _______________
- [ ] Direct license assignment vs group-based - what changes when a user moves department? _______________

---

## Lab 4: Configure SSPR

**Goal:** understand the SSPR configuration surface (full end-to-end user enrolment isn't testable solo without a second real inbox/phone, but the config screens are what the exam probes).

1. **Entra ID > Password reset**.
2. Set **Self service password reset enabled** to *Selected*, and add `sg-assigned-test` as the scoped group.
3. Go to the **Authentication methods** tab - review the options (mobile app notification/code, email, security questions, phone). Set "Number of methods required to reset" to 2.
4. Go to the **Registration** tab - review "Require users to register when signing in" and the registration reminder settings.
5. Go to the **Notifications** tab - review the admin notification toggle for when an admin's password is reset.

**Notes:**
- [ ] What's the minimum number of auth methods you can require? _______________
- [ ] Where would a user go to register their SSPR methods themselves? _______________

---

## Lab 5: Invite a B2B guest user

**Goal:** see exactly what does and doesn't happen when you invite an external identity.

1. **Entra ID > Users > New user > Invite external user**.
2. Invite a second email address you control (a personal Gmail/Outlook works fine), or use a throwaway address.
3. Send the invite, then check the new user object: **Entra ID > Users**, filter by `User type = Guest`.
4. Open the guest's profile - note the `UserPrincipalName` format (`email_domain.com#EXT#@yourtenant.onmicrosoft.com`).
5. Accept the invitation from the invited mailbox if you have access to it, and observe what consent screen the guest sees on first sign-in.
6. Go to **Entra ID > External Identities > External collaboration settings** and review: guest invite restrictions, guest user access restrictions (what a guest can see in the directory by default).
7. **Do not** assign the guest any role yet - confirm (conceptually, or by trying to sign in as them) that an invited guest with no RBAC/app assignment has no access to any resource, only a directory presence.
8. Still in **External collaboration settings**, scroll to **Collaboration restrictions**. Switch it to **Deny list** and add a throwaway domain (e.g. `blocked-example.com`). Confirm the mode switch disables the allow-list fields - this is the mutually-exclusive behaviour worth seeing once, not just reading about.
9. Switch it back to **Allow all domains** (or your original setting) when done, so you don't accidentally lock yourself out of future invites.

**Notes:**
- [ ] What does the guest's UPN look like? _______________
- [ ] What's restricted by default under "Guest user access restrictions"? _______________
- [ ] What happened to the allow-list fields when you switched to deny-list mode? _______________

---

## Lab 6: Azure RBAC role assignments at every scope

**Goal:** the highest-yield lab this week. Assign roles at all four scopes and use Check Access to read the inherited result.

1. Create (or reuse) a management group: **Management groups > Create** - name it `mg-test`.
2. Move your subscription into `mg-test` (**Subscriptions > your subscription > Change management group**).
3. Create a resource group `rg-week1-test` (empty is fine, no resources needed).
4. Assign roles across all four scopes to `bob-test`:
   - **Reader** at the management group `mg-test` (IAM blade on the management group).
   - **Contributor** at the subscription (IAM blade on the subscription).
   - **Owner** at the resource group `rg-week1-test` (IAM blade on the RG).
   - Leave the resource scope alone (no resources exist yet - that's fine, the point is the first three).
5. Go to `rg-week1-test > Access control (IAM) > Check access`, select `bob-test`, and read the result. You should see **all three roles** listed as applying at this scope (Owner explicitly, Contributor and Reader inherited from above).
6. Now go to a *different, unrelated* resource group (or the subscription root) and run Check Access for `bob-test` again - confirm Owner does **not** show up there (it only applies at/below `rg-week1-test`), but Contributor and Reader still do (inherited from subscription and management group respectively).
7. Clean up the role assignments you don't want to keep (IAM blade > Role assignments > select > Remove), but you can leave the management group and resource group in place, they cost nothing.

**Notes:**
- [ ] At `rg-week1-test`, which three roles did Check Access show for bob-test, and why? _______________
- [ ] At the unrelated RG, which roles were still present and which disappeared? _______________
- [ ] Try to explain in one sentence why Owner at the RG doesn't leak upward to the subscription. _______________

**CLI equivalent (bonus):**
```bash
az role assignment create --assignee <bob-object-id> \
  --role "Owner" \
  --resource-group rg-week1-test

az role assignment list --assignee <bob-object-id> --all -o table
```

---

## Lab 7: Administrative units

**Goal:** scope an Entra role to a subset of users, and see how this is a completely different mechanism from Azure RBAC/management groups.

1. **Entra ID > Roles and administrators > Administrative units > Add**.
2. Name it `au-test-region`.
3. Add `alice-test` as a member of the AU (Members tab).
4. Go to the AU's **Roles and administrators** tab > **Add assignments**.
5. Assign `bob-test` the **Helpdesk Administrator** role, scoped to this administrative unit only (not tenant-wide).
6. Confirm the assignment: go to `bob-test`'s user profile > **Assigned roles** - it should show Helpdesk Administrator with the AU listed as the scope, not "Directory".
7. Conceptually confirm: `bob-test` can now reset `alice-test`'s password (she's in the AU) but has no such rights over any user outside `au-test-region` - unlike a tenant-wide Helpdesk Administrator assignment, which would cover everyone.

**Notes:**
- [ ] Where in the UI does an AU-scoped role assignment show as different from a tenant-wide one? _______________
- [ ] In one sentence: how is this different from assigning an Azure RBAC role at a management group? _______________

---

## Wrap-up checklist

- [ ] Lab 1: users created, password reset and block sign-in tested
- [ ] Lab 2: assigned group and dynamic group both created, dynamic rule confirmed working
- [ ] Lab 3: license assignment flow understood (assigned or documented as unavailable)
- [ ] Lab 4: SSPR scoped, auth methods reviewed
- [ ] Lab 5: guest invited, UPN format observed, external collaboration settings and allow/deny list behaviour reviewed
- [ ] Lab 6: roles assigned at 3 scopes, Check Access read correctly at two different resource groups
- [ ] Lab 7: administrative unit created, role scoped to it, scope confirmed on the assignment
- [ ] Can you explain, without looking, why Owner on a subscription is not the same as Global Administrator?
- [ ] Can you explain, without looking, why an administrative unit is not the same as a management group?
