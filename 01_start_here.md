# Start here

This page explains what a Nuvolos Trusted Research Environment (TRE) is and how it is built. It is for every reader, including researchers, project owners, data custodians, output checkers, infrastructure operators and legal reviewers. It shows which protections apply at each level, who acts at each stage, and what Nuvolos does not promise.

## What a Nuvolos TRE is

A **Nuvolos TRE** is a governed project for working with sensitive data. Researchers analyse the data inside the project. Results leave only through a checked process. The environment is one part of a wider arrangement that includes people, data, settings and outputs.

Nuvolos organises work into organisations, spaces and instances. A TRE project is one space with a protection level, and that level applies to everything in the space. Four levels exist:&nbsp;

1. Open (L0),&nbsp;  
2. Controlled (L1),&nbsp;  
3. Locked (L2) and&nbsp;  
4. Enhanced (L3).&nbsp;

Open is ordinary Nuvolos. It is not a TRE. The other three are valid TRE levels.

### The Five Safes

The Five Safes frame the whole arrangement: safe people, safe projects, safe settings, safe data and safe outputs. No single control establishes trust across all five. The table shows what Nuvolos provides for each Safe, and what the organisation provides. Check each deployment's evidence before relying on them.

| Safe          | What Nuvolos provides                                                                                                                                                                                         | What the organisation provides                                                 |
| :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------- |
| Safe people   | Named accounts on the deployment's identity provider. Multi-factor authentication is intended and depends on the deployment's identity configuration. Audit trail records every grant, change and revocation. | Eligibility and training checks, and the named people who approve access.      |
| Safe projects | One space per project, with a server-enforced protection level. Project approval and dataset approval are designed as separate decision records.                                                              | The project's purpose, conditions of use and approval decisions.               |
| Safe settings | The protection level applies to every instance, workload and data path. Network, software and session controls follow the level.                                                                              | Choosing the level that matches the data and its risks.                        |
| Safe data     | An import airlock, versioned read-only datasets, and documented encryption and key custody for each data plane.                                                                                               | The legal basis, the data classification and the accuracy of what is approved. |
| Safe outputs  | An output airlock with a frozen manifest, advisory checks and identity-bound delivery.                                                                                                                        | Qualified, independent checkers, and the data owner's release decisions.       |

&nbsp;

### Shared trust

Nuvolos provides technical controls and evidence. The data controller and the organisation stay responsible for approvals, lawful use, training, checking and oversight. The operator of the deployment may be Nuvolos, the customer or a partner, as the deployment agreement sets out.

### Responsibility posture

Nuvolos states which controls are enforced, which are not, and where responsibility sits. A control counts only where the deployment shows evidence for it. SATRE informs the design. SATRE is a self-assessment of one operated deployment. It is not a certificate for the product.

## How it is built

The platform enforces each mechanism on the *server side*. A rollout setting controls when a level is offered. It never changes what the level enforces.

### Organisation, space and instance

An organisation is the administrative container for a customer. It groups spaces, members, billing and administration. Organisation roles do not approve access to sensitive data.

A space groups work. A TRE project is one space. A dataset space is a different use of a space: it is a curated data asset that holds versioned datasets, not a working environment. An instance is a work area inside a space, holding files and applications. An instance is *never* a security boundary on its own.

### One project, one space

One TRE project is one space. The space carries the protection level, and the level applies to every instance, workload and data path in it. Two different projects stay separated, including where they share platform services.

Moving data between projects, or out of a project, crosses a governed boundary. Creating a snapshot inside a project does not cross one. In a TRE setting, copying or distributing material to another space needs two decisions: a source-space export decision and a destination-space import decision.

### Data planes

Each place where data can sit has its own rules. These places are called data planes. They include instance files, tables, bulk storage, customer-owned storage, snapshots, backups, compute-side scratch space, logs, staging areas and AI artefacts. Each plane is either covered by the project policy or refused.

A data path is anywhere data can sit or move. That covers a data plane, or a route such as a network connection or an integration.

If a deployment cannot cover a plane to the level's standard, that combination is refused at onboarding. A plane is never treated as safe only because it sits inside an instance.

### Import airlock

The import airlock is the governed route for data, code and other inbound material. It applies at Controlled, Locked and Enhanced. Incoming material first lands in a per-request quarantine. No project workload can read, mount or run it there.

Configured checks then run and record their results. A custodian who is not the requester decides: approve, return for changes or reject. The custodian decides under the data owner's authority. Approved material is published as a named, read-only version. A failed or missing required check blocks approval. The import fails closed.

### Output airlock

The output airlock is the governed route for results that leave a project. The requester stages the exact files. The request is bound to a manifest that lists every item with its checksum. Automated checks report against that manifest, but they never decide. A named human checker decides.

Approved bytes go to one authorised recipient, through a single-use link that expires. The link is bound to the named recipient's identity.

Any change to the bytes invalidates the approval. A timeout never releases anything. The table shows the request states.

| State                | Meaning                                                                                                  | Next states                                                                |
| :------------------- | :------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------- |
| Submitted            | The frozen manifest is accepted, and checks are pending or complete.                                     | In review; withdrawn or expired                                            |
| In review            | The assigned checkers are examining the frozen content.                                                  | Decided; expired                                                           |
| Decided              | Approve, return for changes or reject is recorded with reasons.                                          | Delivered (approve); submitted again (return for changes); closed (reject) |
| Delivered            | The authorised recipient retrieved the approved content.                                                 | None                                                                       |
| Withdrawn or expired | The requester closed the request, or the escalation clock (the deadline for an overdue request) ran out. | None; this is never a release                                              |

### Remote-desktop sidecar at Controlled

At Controlled, no application's interface reaches the user's browser directly. Each interactive application, such as a notebook, web IDE, statistical tool or desktop, runs in its own container. A named, unprivileged sidecar in the same workload renders the application in an isolated browser or desktop session (an interactive application session) and streams only the screen to the user.

The application listens only inside the workload, and only the sidecar is reachable from the user's device. The sidecar sets the clipboard and transfer defaults for the session it renders. Each clipboard or transfer attempt is logged with its direction, size and outcome. The log never holds its content.


| Control                                            | Default                                                                              |
| :------------------------------------------------- | :----------------------------------------------------------------------------------- |
| Copy-out from the session to the user's device     | Blocked. This cannot be changed.                                                     |
| Paste-in to the session                            | Allowed up to a size limit, and logged. Project policy can block, limit or allow it. |
| File transfer in either direction                  | Blocked. Files move only through the airlocks.                                       |
| Downloads and printing from the in-session browser | Disabled.                                                                            |
| Direct address of the application                  | Not exposed.                                                                         |

&nbsp;

An application that cannot run behind the sidecar is not offered at Controlled. An exception is possible only when it is recorded on the verdict page.

Nuvolos lists browser surfaces and web IDEs without a server-side control point as uncovered. It does not count them as protected.

### Batch at Locked

At Locked, researchers may only submit analysis code as batch jobs. Each job runs against approved, versioned, read-only inputs, on approved and pinned software, in isolated storage. There are no interactive researcher sessions, no direct internet and no outside model or API calls.

Researchers follow progress and consumption through the run record. Outputs stay inside the project until they pass the output airlock. Output checkers review them in a contained reviewer session, where content can be inspected but not downloaded. AI and ML batch jobs are possible where the approved software and resources allow.

### Audit trail

Audit trail records grants and revocations, approvals, refusals, exports, imports, operator access, agent actions and enforcement changes. Each record names the acting person or AI agent and the decision or event. Records never contain bearer tokens, delivery links, passwords, API keys or sensitive data content.

The trail is append-only and tamper-evident. It is not tamper-proof, and its records may be unsigned. Tenant administrators and auditors can read their own tenant's trail. A tenant may cover more than one organisation. The trail can be exported to the customer's own destination or SIEM. Evidence starts when capture starts. History that was never recorded is not backfilled.

### Verdict page

The verdict page shows one state for each control in each cluster class. A cluster class is the infrastructure the deployment runs on, such as a shared cluster class or a dedicated tenant environment. A state is enforced, not enforced, not proven or not applicable. Missing evidence displays as not proven. Evidence that has gone out of date displays as stale. The page errs towards under-claiming, so it is the reference for what is enforced where.

### Limits

- Nuvolos does not block screenshots, photographs, screen recording or manual retyping at any level.  
- The sidecar controls clipboard and file transfer. It does not control what appears on screen, and streaming adds latency.  
- Paste-in brings data into an interactive session. Project policy decides whether that is allowed. Contained reviewer sessions block it.  
- Instances share their project's level. Narrower instance permissions cannot widen access beyond the project level; whether a narrower role is an enforced read barrier depends on deployment evidence.  
- The audit trail is tamper-evident, not tamper-proof. Verdict claims are made per deployment.

## The four protection levels

Each level adds controls to the one below it. The platform enforces each TRE level for every instance and data path in its project.

|                 | Open (L0)                                     | Controlled (L1)                                                                                                                             | Locked (L2)                                                                                                             | Enhanced (L3)                                                                                                                           |
| :-------------- | :-------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------- |
| Intended use    | Teaching and open science.                    | Interactive research with governed import and export.                                                                                       | Batch analysis of sensitive data under the data owner's conditions.                                                     | Batch analysis that needs dedicated placement and tighter operations.                                                                   |
| Sessions        | Ordinary sessions.                            | Interactive applications, delivered through the remote-desktop sidecar.                                                                     | No interactive researcher sessions. Batch jobs only, plus contained reviewer sessions for checkers.                     | As Locked.                                                                                                                              |
| Software        | Any image the platform offers.                | Supported applications. Additions go through a governed request. An enforced approved-image list is not promised.                           | Approved, pinned software on isolated storage.                                                                          | As Locked, on a dedicated deployment.                                                                                                   |
| Network         | Ordinary platform egress.                     | Policy-defined destinations. Outbound internet is not blocked by default.                                                                   | No direct internet. Only approved essential internal services are reachable.                                            | As Locked, with tighter deployment isolation.                                                                                           |
| AI and agents   | Ordinary platform use, with no TRE assurance. | Agents with their own identity and a named sponsor. Outside model endpoints only under a policy approved by the data owner and the project. | No outside model or API calls. No runtime agents. AI and ML batch jobs allowed where the approved software permits.     | As Locked.                                                                                                                              |
| Import          | Ordinary uploads and integrations.            | Import airlock.                                                                                                                             | Import airlock.                                                                                                         | Import airlock.                                                                                                                         |
| Output checking | Ordinary downloads, links and exports.        | Output airlock, with at least one qualified independent checker.                                                                            | Output airlock, with two independent checkers who both approve, working in a contained reviewer session.                | As Locked.                                                                                                                              |
| Operator access | Existing platform operations.                 | Break-glass only, with a ticket, a second approver, scope, expiry, notice to the tenant and a record.                                       | As Controlled, tightened. Operators can still reach project data under break-glass; operator blindness is not promised. | Scoped, time-limited and dual-authorised. Still not operator-blind.                                                                     |
| Key custody     | Platform default.                             | Platform default, documented.                                                                                                               | Documented custody for each data plane.                                                                                 | Per-plane encryption with documented custody. Customer-managed keys only with full coverage of the storage in scope for the deployment. |
| Deployment      | Ordinary platform.                            | Per deployment, with evidence per cluster class.                                                                                            | Per deployment, with evidence per cluster class.                                                                        | Dedicated deployment.                                                                                                                   |
| Main limit      | No TRE assurance.                             | Pixels can still be captured, and outbound internet is not blocked by default.                                                              | Reviewer sessions are still interactive sessions, and interactive working is not offered to researchers.                | Not operator-blind, not air-gapped, and no confidential computing.                                                                      |

&nbsp;

Limits

- Levels go up with re-approval. They never go down in place. A lower level needs a new space that receives only approved material, moved through the airlocks.  
- Enhanced adds dedicated placement and tighter operator access. It does not add air-gapping, hardware confidential computing or remote attestation.

## Lifecycle of a TRE project

Each project moves through seven stages. Each stage has named actors. No sensitive data enters or leaves a project before the stage that allows it.

1. **Request and approval.** The project owner proposes the purpose, people, datasets, resources and agreement, and names a project manager. Nuvolos records required legal and data-controller decisions separately from the project approval.  
2. **Set up.** An authorised platform user creates the space at the chosen level. The infrastructure operator confirms that the level and resources are supported. Unsupported combinations are refused.  
3. **Import.** A requester submits an import request. Material is quarantined and checked. A custodian who is not the requester decides: approve, return for changes or reject.  
4. **Work.** Researchers use the tools the level permits. At Controlled they work in interactive sessions. At Locked they submit batch jobs and read the run record.  
5. **Output.** The researcher selects the exact files and submits an output request. At Controlled, at least one qualified checker decides. At Locked, two independent checkers must both approve. The data owner or a delegate holds release authority. At Controlled, a checker may hold it only if the data owner delegates it. At Locked, neither checker may exercise it.  
6. **Operate.** Nuvolos records access, approvals, refusals, exports and operator actions. Operators act only under break-glass, with a second approver who is not the operator requesting access.  
7. **Close out.** Access ends. Outstanding outputs leave only through the output airlock. The data custodian and the infrastructure operator dispose of each data plane. The close-out record names any residual copies and their expiry windows.

### Limits

- Nuvolos does not promise a decision time for any request. Waits are measured and shown.  
- Deleting a visible file does not prove that every copy is gone. Backups and replicas may persist until their documented expiry.

## Who does what

Each role has a defined job and a list of things it never does. The target model records assignments per project. No platform role creates a governance role on its own. These governance roles are a proposed target model. The platform enforces each one only where a deployment shows evidence for it.

| Role                    | Does                                                                                                       | Never does                                                                                            |
| :---------------------- | :--------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
| Project owner           | Sets the purpose and terms, nominates the project manager, and owns requirements and budget.               | Approves its own request, or signs for the organisation without separate authority.                   |
| Project manager         | Invites users, changes delegated roles and requests resource changes.                                      | Approves its own changes or widens its own scope.                                                     |
| Data controller         | Decides whether the project may use a dataset, and on what terms.                                          | Gains legal status from a platform role.                                                              |
| Data custodian          | Operates intake and access under the controller's instructions. Approves imports as a non-requester human. | Approves its own request, or approves on an agent's recommendation.                                   |
| Data owner or delegate  | Sets release conditions and holds release authority under the data agreement.                              | Receives release authority from an administrative role alone.                                         |
| Researcher              | Runs approved analysis, submits imports, batch jobs and output requests.                                   | Approves a dataset, or checks its own output.                                                         |
| Output checker          | Examines the frozen content and records approve, return for changes or reject.                             | Checks its own request, or an agent's output that it sponsors. Machine identities are never checkers. |
| Agent sponsor           | Creates, scopes and revokes an agent, and is accountable for what it does.                                 | Checks the output of an agent it sponsors.                                                            |
| Infrastructure operator | Provisions the environment, capacity and guardrails, and acts under break-glass when authorised.           | Reads protected data outside break-glass. Provisioning does not confer data access.                   |
| Auditor                 | Reads the tenant's audit trail and evidence within the agreed scope.                                       | Changes records.                                                                                      |

## Principles

- **Fail closed.** When a check, a checker or capacity is missing, the answer is wait or no. A timeout never releases material.  
- **No self-approval.** A requester never decides their own request. Agents and machine identities never approve, check or release.  
- **Humans decide, checks assist.** Automated checks report evidence against a frozen record. A named person records the decision.  
- **Enforced means enforced.** A control counts only where the platform enforces it and evidence supports it. Warning-only paths are not enforcement.  
- **Evidence over percentages.** Claims rest on evidence for a named deployment. Missing evidence shows as not proven, never as green.  
- **Levels go up, never down in place.** Raising a level needs re-approval. Lowering one needs a new space and an airlock migration.

## What Nuvolos does not promise

- A turnaround time for any approval, check or delivery. Contractual timing, if any, sits in the organisation's service agreement.  
- Certification. SATRE is a self-assessment of one operated deployment.  
- Operator blindness at any level.  
- Universal data residency or fixed retention. Both are documented per deployment.  
- Complete erasure while a copy remains. Deletion is reported per data plane, and residual copies are named.  
- That no data can ever leave a project. Screenshots, photographs and retyping remain possible at every level.  
- <!-- gdoc_comment_begin: c1 -->That outbound internet is blocked by default at Controlled.<!-- gdoc_comment_end: c1 -->  
- Nuvolos does not promise interactive working at Locked or Enhanced. Contained reviewer sessions are contained and logged, but they are still interactive sessions. Output checkers view content on screen, and screenshots, photographs and retyping remain possible.  
- A tamper-proof audit trail. Records are tamper-evident and may be unsigned.  
- Air-gapping, hardware confidential computing or remote attestation at Enhanced.  
- That budgets reserve capacity. A budget is a financial limit, not automatically a hard spending cap. Whether it stops running work depends on the deployment.  
- That a paused agent stops at once. Pause blocks new submissions and dispatches. A running step stops only through a separate action, with an observed outcome.  
- That instructions given to an agent are a security control. Prompt injection is not solved.

## Where to read next

Each guide is written for one reader and stands on its own. Read your own guide first, then the glossary for any term you don't know.

| #    | If you are…                                                               | Read                                                             | You will learn                                                                                                                                     |
| :--- | :------------------------------------------------------------------------ | :--------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| 02   | Project owner, project manager, checker, custodian or space administrator | [02_for_project_teams.md](02_for_project_teams.md)               | Permissions, set-up, access reviews, custodian and checker workflows, resources and budgets, level changes, close-out                              |
| 03   | Researcher or data scientist                                              | [03_for_researchers.md](03_for_researchers.md)                   | Your environment, sessions, software, batch jobs, output requests, disclosure checks, worked examples, budgets, what to do when blocked            |
| 04   | Compliance officer, data protection officer, legal reviewer or auditor    | [04_for_compliance_and_legal.md](04_for_compliance_and_legal.md) | Five Safes mapping, audit records, lifecycle states, governance gates, agreements, separation of duties, SATRE, evidence pack, what is not claimed |
| 05   | Anyone                                                                    | [05_glossary.md](05_glossary.md)                                 | Plain definitions of every term used                                                                                                               |

&nbsp;

