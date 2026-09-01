# Azure Certification Plan: AZ-900 + AZ-104 (2026 Scope)

**Prepared:** 1 September 2026
**Verified against:** Microsoft Learn official study guides (AZ-104 skills measured as of 17 April 2026, AZ-900 skills measured as of 20 July 2026)
**Target candidate profile:** Senior DevOps / Platform Engineer, AWS and Kubernetes native, limited hands-on Azure

---

## 1. TL;DR Recommendation

| Item | Recommendation |
|---|---|
| Do AZ-900 at all? | Yes, but compress it to 6 to 8 hours total. Treat it as a vocabulary sync, not a course. |
| AZ-900 target date | Mid to late September 2026 |
| AZ-104 target date | Late November to early December 2026 |
| Realistic AZ-104 prep effort | 6 to 8 weeks at 6 to 10 hours/week (you have sysadmin depth, just not Azure depth) |
| Biggest risk | Portal muscle memory. You know the concepts from AWS. You do not know where Azure hides them. |
| Total exam budget | Approx USD 264 (AZ-900 USD 99 + AZ-104 USD 165), regional pricing applies at Pearson VUE checkout |

**Sequencing note:** you already have CKA in flight targeting completion before the new role start date (31 Oct). Do not run CKA and AZ-104 in parallel, they compete for the same lab hours. The clean order is:

1. **Sep to Oct:** CKA as the primary focus, AZ-900 slotted in as a low-effort side quest (it needs zero lab time)
2. **Nov to Dec:** AZ-104 as primary, once you have settled into the new role
3. **Q1 2027:** AZ-400 (DevOps Engineer Expert), which AZ-104 unlocks

---

## 2. Verified 2026 Exam Facts

### AZ-900: Microsoft Azure Fundamentals

| Attribute | Value |
|---|---|
| Skills measured version | As of **20 July 2026** |
| Domains | Cloud concepts (25-30%), Azure architecture and services (35-40%), Azure management and governance (30-35%) |
| Passing score | 700 of 1000, scaled scoring |
| Cost | USD 99 (varies by region and tax) |
| Format | Approx 40-60 questions, roughly 85 min seat time |
| Expiry | Fundamentals certs do not expire |
| Delivery | Pearson VUE test centre or OnVUE online proctored |

**July 2026 change log:** Audience profile no change. Only three sub-objectives flagged "Minor": Azure compute and networking services, features and tools for managing/deploying resources, and monitoring tools in Azure. No domain restructure, no weight movement.

### AZ-104: Microsoft Azure Administrator

| Attribute | Value |
|---|---|
| Skills measured version | As of **17 April 2026** |
| Domains | See table below |
| Passing score | 700 of 1000, scaled scoring |
| Cost | USD 165 (varies by region) |
| Format | Approx 40-60 questions, approx 120 min |
| Question types | Multiple choice, multi-select, drag-and-drop ordering, hotspot config screens, case studies |
| Expiry | 12 months, renewed free via unproctored open-book assessment on Microsoft Learn |
| Retake policy | 24 hours after first fail, 14 days after second and subsequent, max 5 attempts per 12 months |

**AZ-104 domain weights (current):**

| Domain | Weight | Priority |
|---|---|---|
| Manage Azure identities and governance | 20-25% | **Highest** |
| Deploy and manage Azure compute resources | 20-25% | **Highest** |
| Implement and manage storage | 15-20% | High |
| Implement and manage virtual networking | 15-20% | High (and the usual killer) |
| Monitor and maintain Azure resources | 10-15% | Medium, but very procedural |

Identity plus compute together account for roughly 40 to 50% of the exam. If you are short on time, that is where the hours go.

---

## 3. What the April 2026 Update Actually Changed

There is a lot of misinformation circulating on this. Several 2026 blogs claim the update added AI service management, Copilot administration, Azure Arc hybrid management and "new" Bicep coverage worth 8 to 15% of questions.

**Microsoft's published change log says otherwise.** Every functional group is marked "No change". Only six sub-objectives got "Minor" edits:

- Audience profile (minor)
- Configure Azure Files and Azure Blob Storage (minor)
- Create and configure virtual machines (minor)
- Provision and manage containers in the Azure portal (minor)
- Configure and manage virtual networks in Azure (minor)
- Monitor resources in Azure (minor)

The identity and governance group is not in the change log at all, meaning Microsoft flagged nothing there. Weights did not move.

**Practical implication:** older material is still usable. Spot-check these four areas against the current objective list before trusting a 2024/2025 course:

1. Blob lifecycle management and blob versioning
2. Encryption at host for Azure VMs
3. Azure Container Apps sizing and scaling
4. Network Watcher plus Connection monitor

**Also note:** Bicep is now explicitly in the audience profile ("ARM templates **or Bicep files**"), and the compute domain tests converting an ARM template to a Bicep file. Given your Terraform background this is a small delta, but the syntax is unfamiliar enough to lose points on a hotspot question.

---

## 4. What 2026 Candidates Actually Report

Aggregated from 2026 exam guides, community write-ups and candidate feedback threads. Treat as directional, not gospel.

**On difficulty and timing**

- Consensus prep time is 4 to 12 weeks part-time at roughly 6 to 10 hours per week. People who already administer Azure daily report the low end (4 to 6 weeks). Coming from on-prem or another cloud only, plan for the top of that range.
- Community consensus puts AZ-104 prep at roughly 10 to 20 times the effort of AZ-900.
- The difficulty is not volume, it is that questions are scenario-based. Knowing what a feature does will not save you if you have never configured it. You get a situation, four plausible answers, and the right one depends on a detail you only notice if you have clicked through the portal yourself.

**On the failure modes people report**

1. **No hands-on lab time.** Reading about VNet peering is not the same as configuring it. This is the single most cited reason for failing.
2. **Underestimating networking.** NSG rule evaluation order, load balancer selection and VPN gateway types are heavily tested. The most frequently named single high-yield topic is **NSG rule evaluation order**.
3. **Not practising case studies.** Case-study sections lock the moment you leave them. Standalone practice questions do not prepare you for a two-page scenario with 5 to 7 dependent questions.
4. **Booking too early to create artificial pressure.** Book at the point where you are consistently scoring 80%+ on timed mocks, not before.

**On format**

- The exam is split into sections with a review screen, but you can only revisit and change answers among the standalone non-case-study questions. Case studies are one-way.
- Live in-exam hands-on labs were retired around 2023, so expect scenario questions, drag-and-drop and hotspot rather than a real portal. Some sources still say labs "may" appear, so check the exam page at booking time.
- Documentation search inside the exam is a safety net for a couple of uncertain questions, not a strategy. It eats time fast.

**On resources people credit for passing**

- **John Savill's AZ-104 Study Cram v2** (approx 4 hours) plus his AZ-104 master class playlist. Named in nearly every write-up. Also the AZ-104 whiteboard PNG on his GitHub.
- **Scott Duffy's Udemy AZ-104 course**, frequently cited by people who passed.
- **Microsoft Learn AZ-104 learning path** plus the official free Practice Assessment.
- **MeasureUp** for the official practice test, or Tutorials Dojo as a cheaper alternative.
- The **Microsoft Learning GitHub labs** (`microsoftlearning.github.io/AZ-104-MicrosoftAzureAdministrator`), which are the actual instructor-led course labs, free.

Ignore anything named "dumps". Half the "I passed" posts you will find are affiliate spam for dump sites, and Microsoft's exam policy treats brain dumps as grounds for certification revocation.

---

## 5. Resource Stack

### Free (this is genuinely enough)

| Resource | Use |
|---|---|
| Official AZ-104 study guide on Microsoft Learn | Source of truth. Copy the skills list into a tracker. |
| Official AZ-900 study guide on Microsoft Learn | Same. |
| Microsoft Learn free Practice Assessment (both exams) | Diagnostic, not a predictor. Run it early to find gaps. |
| Exam sandbox (`aka.ms/examdemo`) | Do this once before exam week so the UI does not cost you time. |
| John Savill AZ-104 Study Cram v2 + playlist + whiteboard | Primary video pass and final revision |
| John Savill AZ-900 full course playlist + handout | Enough on its own for AZ-900 |
| Microsoft Learning GitHub AZ-104 labs | Your lab curriculum, do not invent your own |
| Azure free account (USD 200 credit, 30 days) plus pay-as-you-go | Lab environment |

### Paid (optional, pick one at most)

| Resource | Cost | Worth it if |
|---|---|---|
| Scott Duffy Udemy AZ-104 | approx USD 15 on sale | You want a structured second pass |
| MeasureUp official practice test | approx USD 100+ | You want the closest-to-real question style |
| Tutorials Dojo AZ-104 practice exams | approx USD 15 to 25 | Budget alternative to MeasureUp |
| Exam Ref AZ-104 (Packt / Microsoft Press) | approx USD 40 | You prefer reading to video |

### Voucher hunting

- Microsoft Virtual Training Days regularly hand out free or 50% off vouchers for **fundamentals** exams (AZ-900). Register for an Azure Fundamentals VTD before paying for AZ-900. Voucher lands on your Microsoft Learn profile a few business days after the event.
- Associate-level vouchers (AZ-104) surface via Ignite, Build, Cloud Skills Challenges, employer programs and Microsoft partner orgs. Worth asking your employer whether they have an ESI or partner voucher pool before you pay USD 165 yourself.

---

## 6. Cost Budget

| Line item | Amount (USD) |
|---|---|
| AZ-900 exam | 99 (potentially 0 with a Virtual Training Day voucher) |
| AZ-104 exam | 165 |
| Azure lab spend (2 months, disciplined) | 20 to 60 |
| One practice exam set | 0 to 100 |
| Contingency for one AZ-104 retake | 165 |
| **Realistic total** | **approx 285 to 490** |

Lab cost control: deploy into one resource group per lab, delete the resource group the moment you finish, set a budget alert at USD 10, and never leave a VM, Bastion host, App Gateway or VPN Gateway running overnight. Bastion and gateways are the expensive ones.

---

## 7. Timeline

```
SEP 2026        OCT 2026        NOV 2026        DEC 2026
|---------------|---------------|---------------|---------------|
[CKA primary focus.............]
  [AZ-900 side quest]
     ^ sit AZ-900 (~19 Sep)
                                [AZ-104 primary...............]
                                                    ^ sit AZ-104 (~5 Dec)
                  ^ new role start
```

**Why AZ-104 lands in Nov/Dec, not Oct:** you are serving notice and doing handover through October, and starting a new role at the end of it. Booking AZ-104 in that window is how people end up paying USD 165 twice. The first two weeks in the new role are also the best time to be learning Azure anyway, since you can map exam topics onto the actual estate.

---

## 8. AZ-900 Plan (2 weeks, approx 8 hours total)

You are not the target audience for this exam. Treat it as a terminology sync so that AZ-104 scenario wording does not surprise you.

### Week 1 (approx 5 hours)

| Session | Content | Time |
|---|---|---|
| 1 | Read the official AZ-900 study guide top to bottom. Highlight anything you cannot define in one sentence. | 45 min |
| 2 | John Savill AZ-900 cram, 2x speed, pausing only on flagged items | 2.5 hr |
| 3 | Microsoft Learn Practice Assessment, first attempt, note the domain scores | 1 hr |
| 4 | Fix gaps only. Likely gaps for an AWS person: Microsoft Purview, Azure Arc, Service Health vs Advisor vs Monitor, Entra Domain Services vs Entra ID | 45 min |

### Week 2 (approx 3 hours)

| Session | Content | Time |
|---|---|---|
| 5 | Practice Assessment attempt 2 plus a free third-party mock. Target 85%+. | 1.5 hr |
| 6 | Terminology drill on the AWS-to-Azure map in section 11 | 45 min |
| 7 | Exam sandbox walkthrough, then sit the exam | 45 min |

### The AZ-900 topics that catch experienced non-Azure engineers

These are pure Azure vocabulary with no AWS equivalent that maps cleanly:

- **Microsoft Purview** in Azure (governance and compliance, not a security tool)
- **Azure Arc** (extends Azure management to on-prem and other clouds)
- **Region pairs and sovereign regions** (Azure-specific concept, not the same as AWS AZ pairing)
- **Azure Advisor vs Azure Service Health vs Azure Monitor** (three distinct things, all tested)
- **Entra ID vs Entra Domain Services vs Entra External ID**
- **Availability sets vs availability zones vs VM Scale Sets** (availability sets have no AWS analogue)
- **Consumption-based model, serverless, cloud pricing model comparison** (conceptual questions, phrased in business language)

---

## 9. AZ-104 Plan (8 weeks)

### Ground rules

1. **Every week has lab hours.** If you skip labs you will fail, that is the single most consistent piece of 2026 candidate feedback.
2. **Portal first, CLI second.** Your instinct will be `az` CLI. The exam tests portal blade names and hotspot screens. Do each lab in the portal at least once, then repeat in CLI or Bicep if you want.
3. **One tracker.** Copy the official skills list into a sheet with three columns per skill: *can I do it in the portal*, *can I explain when to use it*, *what is the exam trap*. This is the highest leverage single habit.
4. **Do not book the exam until you hit 80%+ on two consecutive timed mocks.**

### Week 1: Orientation + Identity and Governance (part 1)

**Objectives:** Manage Entra users and groups, manage access to Azure resources

- Watch John Savill cram sections on Entra ID and RBAC
- MS Learn path: Manage identities and governance
- **Labs:**
  - Create users, groups (assigned and dynamic), assign licences
  - Configure SSPR
  - Invite a B2B guest user, observe what changes
  - Assign built-in roles at management group, subscription, RG and resource scope, then read the effective access
- **Trap to internalise:** Azure RBAC vs Entra roles are two different systems. Owner on a subscription does not make you a Global Administrator, and vice versa.

### Week 2: Identity and Governance (part 2)

**Objectives:** Manage subscriptions and governance

- **Labs:**
  - Create a management group hierarchy, move a subscription into it
  - Author and assign a custom Azure Policy (deny a resource SKU, and an `append` or `modify` effect)
  - Apply a `CanNotDelete` lock and a `ReadOnly` lock, try to break them
  - Tag resources, then write a policy that enforces the tag
  - Set a budget with an alert, read Azure Advisor cost recommendations
- **Traps:** Policy vs locks vs RBAC (three different controls, exam loves mixing them). Tag inheritance does not happen by default, you need a policy. Deny effect vs audit effect.
- **Checkpoint:** MS Learn Practice Assessment, first run. Expect to score badly. That is the point.

### Week 3: Storage

**Objectives:** Configure access to storage, configure and manage storage accounts, configure Azure Files and Blob

- **Labs:**
  - Create storage accounts across redundancy options (LRS, ZRS, GRS, RA-GRS, GZRS), note which are changeable after creation
  - Generate a user-delegation SAS and an account SAS, apply a stored access policy, then revoke it
  - Configure storage firewalls and a service endpoint, then a private endpoint, and observe the DNS difference
  - Blob lifecycle management rule (hot to cool to archive), enable versioning and soft delete
  - Azure Files share with identity-based access, plus AzCopy and Storage Explorer transfers
- **Traps:** Which redundancy tiers can be converted in place. Account key vs SAS vs Entra identity-based access. Archive tier rehydration latency. Soft delete for blobs vs containers vs file shares are separate settings.

### Week 4: Compute (part 1, VMs and IaC)

**Objectives:** ARM/Bicep automation, create and configure VMs

- **Labs:**
  - Deploy a VM, then export the deployment as an ARM template
  - Convert that ARM template to Bicep (`az bicep decompile`), read it, modify a parameter, redeploy
  - Resize a VM, attach and expand a managed disk, change disk SKU
  - Enable encryption at host
  - Move a VM to another resource group and to another region
  - Deploy into an availability set, then into availability zones, then a VM Scale Set with autoscale rules
- **Traps:** Availability set (fault/update domains, single datacentre) vs availability zone (separate datacentres) vs region pair. Which VM properties require a deallocate. Encryption at host vs Azure Disk Encryption vs SSE.
- **Bicep note:** you will not write Bicep from scratch on the exam, but you must read it and identify what a given block does. One evening is enough.

### Week 5: Compute (part 2, containers and App Service)

**Objectives:** Containers in the portal, Azure App Service

- **Labs:**
  - Create an Azure Container Registry, push an image, enable admin user vs managed identity pull
  - Deploy the image to Azure Container Instances
  - Deploy the same image to Azure Container Apps, configure scale rules (min/max replicas, HTTP concurrency, KEDA scaler)
  - App Service plan, then scale up vs scale out, then autoscale rules
  - Deployment slots, swap, and slot settings
  - Custom domain plus TLS binding, App Service backup, VNet integration vs private endpoint
- **Traps:** ACI vs ACA vs AKS decision criteria (this is a guaranteed scenario question). Scale up vs scale out. Slot settings that do and do not swap. App Service VNet integration is outbound, private endpoint is inbound.
- **Your advantage:** this domain is where your EKS and Karpenter background pays off conceptually. Just learn the Azure naming.

### Week 6: Networking

The domain most people underestimate. Give it the full week.

**Objectives:** VNets, secure access, name resolution and load balancing

- **Labs:**
  - Two VNets, peering (both directions), test connectivity, then break it and troubleshoot
  - NSGs and application security groups, then read *effective security rules* on a NIC
  - User-defined routes forcing traffic through an NVA or firewall
  - Deploy Azure Bastion, connect to a VM with no public IP
  - Service endpoint vs private endpoint on a storage account, inspect the private DNS zone
  - Azure DNS public zone plus private zone with VNet link
  - Internal load balancer and public load balancer, health probes, backend pools, then deliberately break a probe and troubleshoot
  - Network Watcher: IP flow verify, next hop, connection troubleshoot, Connection monitor
- **Traps to memorise cold:**
  - **NSG rule evaluation order:** priority number ascending, first match wins, default rules last, inbound and outbound evaluated separately, subnet NSG and NIC NSG both apply (inbound: subnet then NIC, outbound: NIC then subnet)
  - Peering is not transitive without a hub NVA or Virtual WAN
  - Load Balancer (L4, regional) vs Application Gateway (L7, regional, WAF) vs Traffic Manager (DNS, global) vs Front Door (L7, global). One scenario question, four plausible answers.
  - Service endpoint keeps a public IP, private endpoint gives a private IP and changes DNS

### Week 7: Monitoring, Backup and Recovery

**Objectives:** Monitor resources, implement backup and recovery

- **Labs:**
  - Azure Monitor metrics on a VM, enable VM Insights, Storage Insights, Network Insights
  - Diagnostic settings routing to a Log Analytics workspace
  - Write basic KQL queries (`AzureActivity | where ... | summarize ...`). You do not need to be fluent, you need to read a query and say what it returns.
  - Alert rule plus action group plus alert processing rule
  - Recovery Services vault, backup policy, back up a VM, restore a file and a full VM
  - Azure Backup vault (this is a separate resource type from Recovery Services vault, and the exam knows it)
  - Configure Azure Site Recovery for an Azure VM, run a test failover
- **Traps:** Recovery Services vault vs Backup vault (different resources, different workloads). Backup vs Site Recovery (data protection vs business continuity). Metrics vs logs. Test failover vs planned vs unplanned failover.

### Week 8: Consolidation and Exam

| Day | Activity |
|---|---|
| 1-2 | John Savill cram v2 full rewatch at 1.5x, whiteboard PNG open beside it |
| 3 | Timed mock 1. Review every wrong answer *and* every guessed-right answer. |
| 4 | Fix the two weakest domains only. Relab anything you cannot do from memory. |
| 5 | Timed mock 2. Target 80%+. If below, push the exam by a week. |
| 6 | High-yield comparison drill (section 10). Exam sandbox. Confirm Pearson VUE booking, ID, room setup. |
| 7 | Light review only, no new material. Sit the exam. |

---

## 10. High-Yield Comparison Drill

Memorise these as decision rules, not definitions. Scenario questions are built on them.

| Comparison | Decision rule |
|---|---|
| Azure RBAC vs Entra roles | RBAC controls Azure resources. Entra roles control the directory (users, groups, apps). Separate systems. |
| Azure Policy vs resource lock vs RBAC | Policy governs *what can exist and how it is configured*. Lock prevents delete/modify regardless of permissions. RBAC governs *who can act*. |
| Management group vs subscription vs resource group | Policy and RBAC inherit downward. Resources live in exactly one RG. RG location stores metadata only. |
| Service endpoint vs private endpoint | Endpoint keeps the public IP and restricts source. Private endpoint injects a private IP and needs private DNS. |
| Load Balancer vs App Gateway vs Traffic Manager vs Front Door | L4 regional / L7 regional with WAF / DNS-based global / L7 global with WAF and CDN. |
| ACI vs Container Apps vs AKS | Single short-lived container / managed serverless microservices with scale-to-zero / full orchestration and control. |
| Scale up vs scale out | Up changes tier or size (usually needs restart). Out adds instances (needs stateless design). |
| Availability set vs availability zone | Fault and update domains inside one datacentre / physically separate datacentres in one region. |
| Backup vs Site Recovery | Point-in-time data recovery / replication and failover for continuity. |
| Recovery Services vault vs Backup vault | Older, broader workload support / newer resource type, different supported workloads. |
| LRS vs ZRS vs GRS vs GZRS vs RA-GRS | 3 copies one datacentre / 3 copies across zones / LRS plus a secondary region / ZRS plus a secondary region / GRS with read access to secondary. |
| ARM template vs Bicep | Same deployment engine. Bicep is the DSL that transpiles to ARM JSON. Bidirectional conversion is testable. |
| Azure Advisor vs Service Health vs Monitor | Recommendations / Microsoft-side incidents affecting you / your telemetry. |

---

## 11. AWS to Azure Translation Map

Your fastest route to Azure fluency is a mapping table, not a beginner course. Beware the "close but not the same" rows, they are where the exam traps live.

| AWS (you know this) | Azure (learn this) | Gotcha |
|---|---|---|
| IAM users/roles/policies | Entra ID + Azure RBAC | Split into two systems. IAM policy JSON has no direct equivalent, RBAC roles are coarser. |
| Organizations / OUs | Management groups | Similar, but policy inheritance model differs. |
| Account | Subscription | Subscriptions are billing plus scope boundaries, and one tenant holds many. |
| VPC | Virtual network | Subnets are regional in Azure, not zonal like AWS. Big difference. |
| Security group | NSG | NSGs are stateful, applied at subnet **and** NIC. Priority-numbered, first match wins, unlike AWS SG evaluate-all. |
| NACL | Roughly NSG at subnet scope | No separate stateless NACL layer in Azure. |
| Route table | Route table with UDRs | System routes exist by default and are invisible until you override them. |
| VPC peering | VNet peering | Not transitive, same as AWS. |
| Transit Gateway | Virtual WAN | Different pricing and topology model. |
| PrivateLink | Private endpoint | Very close. Private DNS zone wiring is the exam detail. |
| VPC endpoint (gateway) | Service endpoint | Not the same as private endpoint. Know the difference. |
| ALB / NLB | Application Gateway / Load Balancer | AppGW is regional only. Front Door is the global L7. |
| Route 53 | Azure DNS + Traffic Manager | Split across two services. |
| S3 | Blob Storage | Storage account is the parent object with its own firewall, redundancy and tier settings. There is no per-bucket equivalent of everything. |
| EBS | Managed disks | |
| EFS | Azure Files | Azure Files supports SMB and identity-based access. |
| EC2 | Azure VM | |
| ASG | VM Scale Sets | |
| ECR | Azure Container Registry | |
| Fargate | Container Instances / Container Apps | ACA is closer to App Runner plus Fargate. |
| EKS | AKS | **Barely on AZ-104.** Do not over-invest here. |
| Elastic Beanstalk / App Runner | App Service | Deployment slots have no clean AWS analogue. Learn them properly. |
| CloudFormation | ARM templates | |
| CDK / Terraform | Bicep | You will read it, not write it. |
| CloudWatch metrics + logs | Azure Monitor (metrics) + Log Analytics (logs, KQL) | KQL is not SQL and not CloudWatch Insights syntax. |
| CloudTrail | Azure Activity Log | Routed via diagnostic settings. |
| AWS Backup | Azure Backup + Recovery Services vault | |
| Cost Explorer + Budgets | Cost Management + budgets + Advisor | |
| Config + SCPs | Azure Policy | Policy does both drift detection and prevention. Effects (deny, audit, append, modify, deployIfNotExists) are testable. |
| Systems Manager Session Manager | Azure Bastion | Bastion is a deployed, billed resource in its own subnet named `AzureBastionSubnet`. |
| VPC Flow Logs | NSG flow logs / Network Watcher | |
| No equivalent | **Availability sets** | Learn from scratch. |
| No equivalent | **Microsoft Purview**, **Azure Arc**, **region pairs** | Learn from scratch. |

---

## 12. Exam Day Checklist

- [ ] Run the Pearson VUE OnVUE system test at least 24 hours before, on the exact machine and network you will use
- [ ] Government ID with name matching your Microsoft Learn profile exactly
- [ ] Private room, clear desk, no second monitor, no phone within reach
- [ ] Check in 30 minutes early, the check-in process itself takes time
- [ ] Read every case study fully before answering, you cannot go back to a case study section
- [ ] Flag and move on. Do not burn 5 minutes on one question with 55 to go.
- [ ] Use the review screen at the end of each non-case-study section
- [ ] Results appear immediately, with a per-domain breakdown

---

## 13. After AZ-104

| Next | Why |
|---|---|
| **AZ-400 (DevOps Engineer Expert)** | Direct fit for your role. AZ-104 or AZ-204 is the prerequisite. Pipelines, IaC, release strategy, monitoring. Q1 2027. |
| **AZ-305 (Solutions Architect Expert)** | Alternative path if you want architecture rather than delivery. Also builds on AZ-104. |
| **AZ-700 (Network Engineer)** | Only if Wilhelmsen's estate is networking-heavy. Savill has a cram for this too. |
| **Renewal** | AZ-104 expires in 12 months. Renewal window opens 6 months before expiry, free unproctored open-book assessment on Microsoft Learn, unlimited attempts inside the window. Let it lapse and you pay the full USD 165 again. Set a calendar reminder the day you pass. |

---

## 14. Progress Tracker

### AZ-900

- [ ] Read official study guide (20 July 2026 version)
- [ ] Savill AZ-900 cram complete
- [ ] Practice Assessment run 1
- [ ] Practice Assessment run 2 at 85%+
- [ ] Voucher checked (Virtual Training Day)
- [ ] Exam booked
- [ ] **Passed**

### AZ-104

- [ ] Skills list copied into tracker sheet
- [ ] Azure subscription live with budget alert set
- [ ] Week 1: Identity part 1
- [ ] Week 2: Governance
- [ ] Week 3: Storage
- [ ] Week 4: Compute (VMs, Bicep)
- [ ] Week 5: Compute (containers, App Service)
- [ ] Week 6: Networking
- [ ] Week 7: Monitoring, backup, recovery
- [ ] Savill cram v2 full rewatch
- [ ] Timed mock 1
- [ ] Timed mock 2 at 80%+
- [ ] Exam sandbox walkthrough
- [ ] Exam booked
- [ ] **Passed**
- [ ] Renewal reminder set for 6 months out

---

## 15. Source Notes

Primary sources (authoritative):

- Study guide for Exam AZ-104, Microsoft Learn, skills measured as of 17 April 2026, page last updated 19 March 2026
- Study guide for Exam AZ-900, Microsoft Learn, skills measured as of 20 July 2026, page last updated 22 June 2026
- Microsoft Learn certification renewal and exam scoring pages

Secondary sources (candidate reports and 2026 exam guides), used for prep-time estimates, failure modes and resource recommendations. These vary in quality and several contradict Microsoft's own change log on the April 2026 update. Where they conflict, the official study guide wins.

**Verify before booking:** re-read the official study guide the week you book. Microsoft can push an update between now and December, and the change log at the bottom of the page is the fastest way to see what moved.
