# For Compliance and Legal

This document is for compliance officers, data protection officers, legal reviewers, auditors and information governance staff. It sets out what evidence a Nuvolos Trusted Research Environment (TRE) produces, how decisions are recorded, who holds authority, and what Nuvolos does not claim.&nbsp;

## The Five Safes and how Nuvolos maps to each

Nuvolos supports each of the Five Safes with a platform control, a record or a gate. Each safe also depends on duties that stay with the organisation.

| Safe          | What Nuvolos provides                                                                                                                                            | What the organisation must do                                                                                             |
| :------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------ |
| Safe people   | Unique accounts, multi-factor authentication through the identity provider, a role model, and training records that can gate sensitive access                    | Verify identity, run onboarding and training, and review access on a schedule                                             |
| Safe projects | One TRE project maps to one space. Project and dataset approvals gate access, and the roster shows why each person has access                                    | Decide eligibility and purpose, name the project owner and manager, and keep the agreement current                        |
| Safe settings | A protection level for each project: Controlled (L1), Locked (L2) or Enhanced (L3). The level applies to every instance, workload and data path in the project   | Choose the level, confirm the network controls the deployment enforces, and approve any change of level                   |
| Safe data     | An import airlock with quarantine, checks that assist, a custodian decision, and a read-only versioned dataset. A failed or missing required check blocks intake | Appoint the custodian, obtain the data controller's agreement, and set the conditions of use                              |
| Safe outputs  | An output airlock that stages exact bytes, freezes a checksummed manifest, runs advisory disclosure checks, and leaves the decision to a person                  | Appoint eligible output checkers, name the release authority, and set a policy for outputs that cannot be checked by hand |

&nbsp;

Locked (L2) runs batch work only. It has no interactive researcher sessions, no internet access, no outside model or API calls and no runtime agents. Enhanced (L3) is Locked plus a dedicated deployment, tighter operator access, and per-data-plane encryption with documented key custody.

### Limits

- Nuvolos raises a level only with re-approval. It never lowers a level in place; a move to a lower level needs a new space and an airlock migration of approved material only.  
- Nuvolos does not block screenshots, retyping, or copying by a person who can already see the data. L2 and L3 mitigate this by disallowing interactive interaction with data.  
- Enhanced is not operator-blind, not an air gap, and does not use confidential computing.  
- Residency, retention and key custody are set per deployment. Nuvolos does not offer one universal figure.

## Controlled (L1) session and transfer controls

In Controlled (L1), no application interface is served directly to a browser on the user's device. A remote-desktop sidecar sits between each application and the user. The sidecar is the only part of the workload that the user can reach.

In this section, session means the interactive application session that the sidecar renders, not a platform sign-in session.

The session works in four steps:

1. Each interactive application runs in its own container. Interactive applications follow this pattern where a server-side control point exists. Nuvolos lists web IDEs and browser surfaces without one as uncovered.  
2. A named, owned, unprivileged sidecar in the same workload renders the application. Web applications appear in an isolated browser. Desktop applications appear in a desktop session.  
3. The sidecar streams the screen to the user. The application listens only inside the workload, and no direct application address is exposed.  
4. On covered channels, clipboard and transfer attempts are checked against the session settings and logged. Check deployment evidence for channel coverage.

| Control                                                              | Default                                  | Who can change it                                                  |
| :------------------------------------------------------------------- | :--------------------------------------- | :----------------------------------------------------------------- |
| Copy-out from the application session to the user's device           | Blocked. This cannot be changed.         | Check deployment evidence for configurability                      |
| Paste-in to the session                                              | Allowed up to a size limit, and logged   | Project policy can block, limit or allow it                        |
| File transfer, in both directions                                    | Blocked. Files move through the airlocks | Product default; check deployment evidence for any configurability |
| Downloads and printing from the isolated browser inside the workload | Disabled                                 | Product default; check deployment evidence for any configurability |
| Direct application address                                           | Not exposed                              | Product default; check deployment evidence for any configurability |

On covered channels, clipboard and transfer audit entries record direction, size and outcome, never content. Deployment evidence must identify covered channels.

**Example.** A researcher works in a notebook in Controlled (L1). They try to copy a result to a laptop. The copy-out is blocked, and the audit trail records the attempt, not the content. A file they try to paste in is allowed only as far as project policy permits.

At Locked (L2) and Enhanced (L3), the contained reviewer session uses the same sidecar. Output checkers use it to inspect staged content, and it is the only interactive session at those levels. Paste-in is also blocked in that session.

### Limits

- Only channels covered by deployment evidence can be counted as controlled. Clipboard and file-transfer controls do not control pixels. Screenshots, screen recording, photographs, retyping and on-device text recognition remain possible.  
- Paste-in brings data into the session. It is logged, and it is blocked only where project policy says so.  
- Streaming adds latency to interactive work \- the trade-off for security.  
- An application that cannot run behind the sidecar is not offered in Controlled. An exception applies only when it is recorded on the verdict page.

## Evidence you can expect

Each deployment produces the evidence below. Every item has a stated scope, date and owner in the deployment documents.

| Evidence                     | What it shows                                                                                                     | Limit                                                                                                                                                           |
| :--------------------------- | :---------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Audit trail                  | Who acted, when, and in which project, including refusals and failed actions                                      | Tamper-evident, not tamper-proof                                                                                                                                |
| Chain status                 | A statement that the audit trail's chain is verified through a stated date, and the date from which records exist | Records start when capture starts; earlier history is not reconstructed                                                                                         |
| Control records              | A fixed record shape for access, level changes, export decisions, and machine and agent actions                   | Completeness is claimed per control; a control with no writer is listed as a gap                                                                                |
| Decision receipts            | For each released or refused output: the decider, time, reason and fingerprint of what was reviewed               | Unsigned; not cryptographic proof of release                                                                                                                    |
| Governance decision records  | Agreement versions, approvals, refusals, expiries, and the recorded roles that decided                            | Records what people decided; does not create legal authority                                                                                                    |
| Roster and key-custody views | Who has access, why (explicit, derived or automatic), at which level, and which keys they hold                    | Accuracy depends on the grant data; unverifiable rows are marked, not guessed. Today's roster can understate derived access. It is not a complete access review |
| Verdict page                 | One state per control: enforced, not enforced, not proven or not applicable                                       | Missing evidence shows as not proven; old evidence shows as stale                                                                                               |
| Key-custody map              | For each storage type: covered bytes, key holder, rotation, subprocessor, region and last verification            | Unresolved custody is shown as unresolved                                                                                                                       |
| Subprocessor register        | Each vendor, its purpose, data classes, region and a named owner                                                  | Unrecorded entries are marked; confirm completeness before relying on it                                                                                        |
| Deletion record              | What was removed on each data plane, what remains, and until when                                                 | Reported per plane; no complete-erasure claim while a residual copy exists                                                                                      |
| SATRE self-assessment pack   | A versioned assessment of one operated environment, with dated evidence for each filled cell                      | A self-assessment, not a certification                                                                                                                          |

### Limits

- Nuvolos does not backfill history that was never recorded.  
- Nuvolos shows a missing control as not proven, never as met.

## Evidence pack contents

The evidence pack is a set of documents that Nuvolos releases to the organisation under its agreement. Every document states its scope, version and date.

| Item                             | Contents                                                                      | Format                                                  | Refresh cadence                               |
| :------------------------------- | :---------------------------------------------------------------------------- | :------------------------------------------------------ | :-------------------------------------------- |
| SATRE self-assessment pack       | Scores, pinned specification version, dated evidence per filled cell          | Versioned document; per deployment                      | Per assessment                                |
| Key-custody map                  | Covered bytes, key holder, rotation, subprocessor, region, last-verified date | Generated from one source and checked for drift         | Per entry; cadence per deployment             |
| Subprocessor register            | Vendor, purpose, data classes, region, named owner                            | Per deployment                                          | Per deployment                                |
| Governance decision records      | Agreement versions, approvals, refusals, expiries, deciding roles             | Per deployment                                          | Per decision                                  |
| Decision receipts                | Decider, time, reason, fingerprint of the content reviewed                    | Recorded; unsigned                                      | Per decision                                  |
| Audit trail export               | Trail entries with the chain head, and the chain status statement             | Encrypted, with a documented decryption procedure       | Scheduled per deployment; or pulled on demand |
| Roster and effective-access view | Who can reach the project, each dataset and instance, and why                 | Per deployment                                          | Per deployment                                |
| Verdict page                     | One state per control; stale evidence marked                                  | Derived from the evidence the enforcement decision uses | Per deployment                                |
| Deletion record                  | Per data plane: deleted, retained, or residual until a stated point           | Per deployment                                          | Per close-out                                 |

&nbsp;

### Limits

- The pack reports evidence. The organisation reviews it and decides what assurance to accept.  
- A scheduled export shows its last successful delivery. A failed delivery raises an alert and does not mean the file arrived.

## Audit trail

The audit trail records each governed action, refusal and failure as an entry in an append-only sequence. Each entry names the real actor, the subject, the scope, the before and after state, the decision and reason, and the outcome. A failed or partial action is never recorded as a success. A retry is a separate entry.

No audit field holds a bearer token, invitation or delivery link, password, API key, session secret or sensitive data content. A field may reference a link identifier, but never the link itself.

Tenant administrators and auditors read the records in their own tenant. A tenant is the deployment-defined scope, and it may span more than one organisation. A dedicated auditor role and a full TRE audit viewer are not available today.

Platform operators (Nuvolos or the operator the deployment agreement designates) use a separate operator-only platform trail. It is not the tenant view. Operator access to tenant audit trails is still proposed. It must be reconciled and scoped before anyone relies on it. Operators cannot edit or delete audit records.

### Audit record fields

| Field               | Meaning                                                                                                                  |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------- |
| Time of event       | The actual time of the event, in UTC. Not the time of a later summary or export                                          |
| Real actor          | The person, service or agent that triggered the action                                                                   |
| Acting for          | The identity the action ran under, when an approved delegation or impersonation applied. Blank when it matches the actor |
| Actor type          | Person, service or agent. Machine and agent actions are attributable, never anonymous                                    |
| Surface             | The route that carried the action: user interface (UI), programming interface (API), command line or scheduled task      |
| Subject             | A typed reference to the project, space, instance, dataset, request or person                                            |
| Scope               | The role, dataset version, recipient or data plane that the event covers                                                 |
| Before and after    | The previous and new state for role and policy changes. The previous state is never overwritten                          |
| Decision and reason | Approve, return for changes or reject, with a reason code and text. Refusals carry reasons too                           |
| Outcome             | Applied, refused, failed or pending                                                                                      |
| Request reference   | Groups all events that belong to one process                                                                             |

Separation-of-duty checks test the real actor. They also test the identity the action ran under.

### Event classes covered

Break-glass is the governed route for operator access to protected data. It is defined in this table and applies in the roles section below.

| Event class                     | Examples                                                             | What is recorded                                              |
| :------------------------------ | :------------------------------------------------------------------- | :------------------------------------------------------------ |
| Authentication                  | Sign-in to the platform                                              | Actor, time, surface, outcome                                 |
| Access-control changes          | Role grants, role changes, revocations                               | Before and after state, scope, origin                         |
| Data access and egress          | Access to a dataset or instance, export and delivery events          | Subject, scope, recipient, outcome                            |
| Invitations and requests        | Sent, accepted, revoked, withdrawn                                   | Subject, role, outcome                                        |
| Governance assignments          | Nomination, approval, acceptance, expiry                             | Subject, duty, scope, decider                                 |
| Decisions                       | Approve, return for changes, reject                                  | Decision, reason, the exact version decided                   |
| Refusals and failures           | Refused attempts, including self-approval; failed or partial actions | Reason; the attempt stays on the record                       |
| Level and enforcement changes   | Level changes, a control switched off, a bypass added or removed     | Before and after state, owner, expiry                         |
| Clipboard and transfer attempts | Copy-out and paste-in on covered Controlled-session channels         | Direction, size, outcome; never the content                   |
| Break-glass actions             | Operator access to protected data                                    | Ticket, second approver, scope, expiry, notification, outcome |
| Agent and machine actions       | Submissions, refusals and state changes                              | Agent identity, run, sponsor                                  |
| Agreement changes               | New versions, signatory entries, expiries                            | Version, parties, scope, term                                 |
| Deletion and close-out          | Per-plane disposition                                                | Planes deleted, retained or residual, and the residual window |
| Pauses                          | Stop controls on automated work                                      | Principal (the paused agent identity), scope, actor           |

The trail covers these classes. A class with no writer in a deployment is listed as a gap.

### Export and off-platform delivery

The organisation can hold the trail outside Nuvolos. A scheduled, encrypted export carries the trail with the chain head. The organisation can also pull records through a cursor-based interface. A failed delivery raises an alert, which does not confirm that the file arrived. The organisation receives a documented procedure to decrypt and verify what it gets. The trail can also feed the organisation's own security information and event management system.

### Honest properties

- **Tamper-evident.** Records are chained by an unkeyed digest. Someone who can rewrite rows and recompute the chain can defeat it. Single-row tampering is detectable.  
- **Starts when capture starts.** The trail cannot reconstruct earlier history.  
- **Retention per record class.** The deployment states how long each class of record is kept.  
- **Unsigned.** Receipts and entries are not signed.  
- **Completeness per event class.** Where a control has no writer, the gap is listed.

### Limits

- Nuvolos does not describe the trail as tamper-proof or immutable.  
- Nuvolos does not claim operator blindness. Operator access is accountable and time-limited.

## Lifecycle and request states

Each governed process has one current-state record. That record says where the process is now, who holds the next action, and what it waits for. The audit trail holds the history of the same process.

### Project lifecycle

| State                | Meaning                                                                                              | Next states                                                                               | Gate to move on                       | Protected work                                       |
| :------------------- | :--------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------- | :------------------------------------ | :--------------------------------------------------- |
| Draft or requested   | Purpose, people, data, level and budget are described                                                | Awaiting decisions; Refused or withdrawn                                                  | None to submit                        | None; no sensitive data                              |
| Awaiting decisions   | Agreement, data approvals, legal review where required, and readiness are outstanding                | Active; Refused or withdrawn                                                              | Project creation and activation gate  | None                                                 |
| Active               | All required decisions are present and valid, the environment is ready, and grants are issued        | Suspended; Close-out requested                                                            | Each action still passes its own gate | Yes, inside approved scope                           |
| Suspended            | A condition failed: agreement expired or withdrawn, access review failed, incident, or resource stop | Active, once the failed condition clears and a valid decision exists; Close-out requested | Required decisions valid again        | No new protected work                                |
| Close-out requested  | The project is ending; outputs are resolved; disposition is agreed                                   | Closed                                                                                    | Deletion and close-out gate           | Winding down; releases still pass the output airlock |
| Closed               | Access revoked; per-plane disposition and residual windows recorded                                  | None (end state)                                                                          | Deletion and close-out gate passed    | None                                                 |
| Refused or withdrawn | The decision was no, or the requester withdrew                                                       | None (end state)                                                                          | Not applicable                        | None; reasons and evidence kept                      |

### Request states

Access, import, export, transfer and deletion requests share one state grammar.

| State                  | Meaning                                                                                       | Next states                                            | Gate to move on                                                                                               |
| :--------------------- | :-------------------------------------------------------------------------------------------- | :----------------------------------------------------- | :------------------------------------------------------------------------------------------------------------ |
| Submitted              | Request recorded with requester, scope and reason                                             | Checks running; Cancelled or withdrawn                 | Intake only; submission grants nothing                                                                        |
| Checks running         | Required checks run; every outcome is recorded, including failed and not performed            | Awaiting decisions; Held; Rejected                     | Required checks pass. An import can proceed past an unconfigured check only on a recorded human risk decision |
| Awaiting decisions     | Required human decisions are outstanding                                                      | Decided; Expired or superseded; Cancelled or withdrawn | Required decisions are present, in scope and valid                                                            |
| Decided                | Approve, return for changes or reject, with reasons                                           | Effective or delivered; Submitted again; Closed        | The approval binds to one scope and version                                                                   |
| Effective or delivered | The action happened: access granted, import published, output retrieved, or deletion executed | Revoked; Expired or superseded                         | Delivery goes only to the named recipient                                                                     |
| Revoked                | An authorised actor ended a grant or approval early                                           | None for that grant                                    | New dependent work is refused                                                                                 |
| Failed or partial      | The attempt ran but did not achieve its effect                                                | Retried as a new attempt                               | Nothing counts as complete                                                                                    |
| Cancelled or withdrawn | The requester or an administrator stopped the request                                         | A new request may be filed                             | The effect must be observed                                                                                   |
| Expired or superseded  | Validity or applicability ended before use                                                    | A new request is required                              | The gate blocks until a new decision exists                                                                   |

### Limits

- A transition is not complete until the authoritative record holds it.  
- A queue, a dashboard strip or a wait-time statistic measures progress. It is not a legal record.  
- A disagreement between the current-state record and the audit trail is a defect. The deployment reconciles it and raises an alert.

## Governance gates

A gate lets a protected action proceed only when the required decisions are present, valid and in scope. Seven gates apply.

| Gate                                         | Decisions required                                                                                                                                 | Notes                                                                                                                                                                                                                                                                         |
| :------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Project creation and activation              | Project owner accountability, agreement and data approvals, legal review where policy requires it, and environment readiness                       | Protected work does not start until these are present                                                                                                                                                                                                                         |
| Access grant                                 | Project approval for the person, dataset approval, and any training or eligibility condition                                                       | An invitation is not a grant                                                                                                                                                                                                                                                  |
| Import                                       | Custodian decision for the exact dataset version, after checks; controller or asset-owner conditions                                               | A failed or missing required check blocks intake; a check that was never configured proceeds only with the intake policy and a recorded human risk decision. For external data entering its first protected project, the source's own release procedure must also be recorded |
| Export and release                           | Disclosure review by the required independent checkers; release authority of the data owner or delegate; delivery to a named recipient             | A missing checker holds the request. A missing advisory check goes to a person and is not a pass                                                                                                                                                                              |
| Cross-project or cross-organisation transfer | A source export decision, the source data owner's authorisation of the named destination and recipient, and a separate destination import decision | Neither decision substitutes for the other                                                                                                                                                                                                                                    |
| Deletion and close-out                       | The organisation's disposition decision per data plane; custodian and operator execution; legal or retention review where policy requires          | Never claims complete erasure while a copy remains                                                                                                                                                                                                                            |
| Configuration change                         | A change to gate policy, protection level or approval requirements                                                                                 | Recorded. A change cannot weaken minimum controls or lower a level in place                                                                                                                                                                                                   |
| Resource change                              | Recorded request and an authorised decision for new capacity, budget mappings or sizes                                                             | Today no approval gate covers resource creation, mapping or size enablement. Not counted among the seven gates until enforced                                                                                                                                                 |

The gate rules are:

- **Empty means blocked.** If a gate needs a reviewer or approver and none is assigned, the action holds with a visible reason. Nuvolos never approves for lack of an approver.  
- **No self-approval.** A requester never approves their own request, grants their own access, or approves their own import or export. Neither the requester nor the executor of a governed action approves it.  
- **Agents never decide.** Agents and machine identities never approve, check, release or sign.  
- **Humans decide; checks assist.** Automated disclosure checks inform a person. They do not approve.  
- **Decisions carry scope.** A decision names its project, dataset version, recipient and data plane. Scope and validity are checked when the gate is used.  
- **One vocabulary.** The three outcomes are approve, return for changes and reject. The requester can also withdraw.  
- **Enforced means enforced.** Warning-mode controls, log-only rules and policy text do not stop an action. A deployment states which gates are enforced, which only observe, and which are not in place.

### Import intake sequence

1. **Request.** A project member states what comes in, where from, why, and the version it becomes.  
2. **Quarantine.** The bytes land in a per-request area that no project workload can read, mount or execute.  
3. **Checks.** Configured checks run. Each outcome is recorded, including checks that were not configured or could not inspect the item.  
4. **Fail closed.** A required check that fails or cannot run blocks promotion. A check that was not configured can proceed only if the intake policy permits it and a non-requester human records the risk decision.  
5. **Custodian decision.** An authorised custodian approves, returns for changes or rejects with reasons. The requester or executor cannot approve their own action. No agent can decide. Under the proposed profile policy, Locked (L2) also needs data-owner approval for new datasets. Enhanced (L3) needs a separate data-owner decision.  
6. **Publication.** Approved material becomes a named, read-only dataset version. The record binds it to checksums or a versioned table identifier, with the source, request, approver, decision and date.

### Release sequence

1. **Refusal and redirect.** An ordinary export route refuses with a reason. The refusal opens a submission prefilled with the refused items.  
2. **Staging.** The requester places the exact output set in the project's staging area.  
3. **Frozen manifest.** The request binds to a manifest that lists every staged item with a checksum. Anything staged but not listed goes to human review as a coverage gap.  
4. **Advisory check.** Checks produce a report against the manifest. A missing report is labelled check not performed. It is never a pass.  
5. **Human review.** Checkers see the frozen manifest, the check results and a comparison with earlier releases. At Locked (L2) and Enhanced (L3), the output checker works in a contained reviewer session: direct download and export are blocked, while screenshots and retyping remain possible. At Controlled (L1), the output checker uses an ordinary platform identity and views material inside the project. No contained reviewer session is guaranteed at L1.  
6. **Decision.** The checker approves, returns for changes or rejects. Overdue requests escalate or expire. They never release automatically.  
7. **Release authority.** At Locked (L2) and Enhanced (L3), the data owner or an authorised delegate authorises release and names the recipient. Neither output checker can be that authoriser. At Controlled (L1), an eligible output checker may hold separately delegated release authority. A checker's approval does not release content on its own.  
8. **Delivery.** Approved content goes to the authorised recipient through an identity-bound, expiring, single-use link. An interrupted transfer is recorded as not complete.  
9. **Revision.** Any change to the bytes invalidates the manifest and the approval. The new content is manifested and reviewed again.

### Limits

- Nuvolos does not promise a turnaround time for any gate. Waits are measured and shown.  
- Nuvolos does not require legal review for every gate. The organisation's policy decides.  
- A recorded approval shows who decided and when. It does not show that processing is lawful.  
- A retrieval record does not prove that the recipient deleted later copies.  
- Nuvolos does not promise automated detection of differencing risk across several releases. The human decision covers it.  
- Trained model artefacts do not leave by default. The project policy, set before training begins, decides whether they may.  
- An output that cannot be meaningfully inspected stays inside the project unless the project policy permits its release.

## Agreements and signatories

Nuvolos holds a record for each agreement that a project relies on. The record shows which version applied, who signed, for what scope, and until when. Today, agreements live outside the platform.

| Field               | What is recorded                                                                             |
| :------------------ | :------------------------------------------------------------------------------------------- |
| Parties             | The legal organisation and the counterparty, not only a person's account                     |
| Signatory           | The named person, declared capacity, date and evidence reference                             |
| Version             | A version identifier and date. Earlier versions stay in the record                           |
| Scope               | Project, datasets and versions, purpose, protection level and permitted recipients           |
| Conditions and term | Use conditions, permitted outputs, retention terms, effective date and expiry or review date |
| Status              | Draft, signed, effective, superseded, expired or terminated                                  |

Agreement lifecycle

| State      | Meaning                                                       | Next states                     | Effect on gates                                                |
| :--------- | :------------------------------------------------------------ | :------------------------------ | :------------------------------------------------------------- |
| Draft      | Terms and parties are drafted; not signed                     | Signed; Terminated              | No gate can rely on it                                         |
| Signed     | Signatory, capacity, date and document reference are recorded | Effective; Terminated           | Not in force; gates do not rely on it                          |
| Effective  | In force from its effective date until expiry                 | Superseded; Expired; Terminated | Gates rely on its scope and conditions                         |
| Superseded | Replaced by a later version; kept in the record               | None                            | Approvals bound to it follow the material-change rule          |
| Expired    | The term has ended                                            | Superseded by a renewed version | Dependent gates block actions that lack valid authority        |
| Terminated | Ended before its expiry                                       | None                            | Dependent gates block; existing access is suspended per policy |

Two events change an agreement outside a simple sequence. A material change to parties, scope, conditions or term sends the affected approvals back for review. A non-material correction follows the organisation's documented policy and does not extend an approval.

A project owner who signs as an authorised signatory does not approve their own access or export. Any later request still needs an independent approver.

### Limits

- Nuvolos records who signed and under what claimed authority. It does not verify that the signatory could bind the organisation.  
- Nuvolos provides no digital-signature service and no qualified signatures.  
- Nuvolos does not decide whether a document is legally sufficient. A chat message or verbal review is not a decision record.  
- Signing outside Nuvolos is recorded by an authorised person, with the document reference, before the gate activates.

## Roles and separation of duties

Platform roles and governance assignments are separate. A platform role says what the software allows. A governance assignment says who is accountable for a decision.

Three rules apply throughout:

- **A name is not an authority.** Creator and owner labels and administrator roles are metadata. They are not legal roles.  
- **Legal and controller roles come from the organisation.** Nuvolos records a nomination and its scope. It does not confer the role.  
- **Combined roles follow the stricter rule.** Where one person holds two roles, the stricter rule applies to each sensitive action.

### Duties

| Duty                                                             | What it decides                                                                         | Boundary                                                                                                                                                                                                            |
| :--------------------------------------------------------------- | :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Data controller                                                  | Whether a project may access a dataset, and on what terms                               | Designated by the organisation; not a platform role                                                                                                                                                                 |
| Information asset owner                                          | Dataset conditions, permitted uses and outputs                                          | Authority comes from the organisation's agreements. The asset owner, data owner and data provider may be one party or several. Release authority follows the agreement and recorded delegations                     |
| Data custodian                                                   | Intake, versioning and access under the data controller's or asset owner's instructions | Administration alone is not data-use authority                                                                                                                                                                      |
| Project owner                                                    | Purpose, terms, and nomination of the project manager                                   | Signs for the organisation only with separately granted authority                                                                                                                                                   |
| Project manager                                                  | Invitations and roles within delegated scope                                            | Cannot approve their own request or widen their own scope                                                                                                                                                           |
| Legal reviewer (optional)                                        | Whether approval conditions are met at a policy checkpoint                              | Appointed by the organisation; recuses where conflict rules require it. Is not an output checker. Gains no research-data access from this role, and reads only the agreement and request metadata for its decisions |
| Data protection officer (optional)                               | Advice and oversight within the organisation's mandate                                  | Does not approve every action                                                                                                                                                                                       |
| Checker                                                          | Disclosure review of staged output                                                      | Never the requester, the agent's sponsor, or any agent                                                                                                                                                              |
| Delegate                                                         | The specific authority delegated, and nothing wider                                     | A named human, not the requester, with recorded scope and dates                                                                                                                                                     |
| Infrastructure operator (the party that runs the infrastructure) | Environment provisioning, capacity and unsupported changes                              | Only as the deployment agreement assigns; not a data-access authority                                                                                                                                               |

Governance assignments are recorded with scope, nominator, start, end and status. Nuvolos enforces an assignment's requirements only where the deployment enforces them server-side.

### Separation-of-duties matrix

The matrix summarises the rules in this section.

| Role                    | Can request                                                       | Can approve                                                                                        | Cannot                                                                                                                 |
| :---------------------- | :---------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------- |
| Requester               | Create and submit requests; respond to a return for changes       | Nothing on their own request                                                                       | Approve their own request; check their own output; receive output unless separately authorised                         |
| Project owner           | Propose purpose, datasets and terms; nominate the project manager | Project purpose and terms; the nomination                                                          | Approve their own access or export; sign for the organisation without separate authority                               |
| Project manager         | Invite users and request resource changes within scope            | Role changes within delegated scope, once required approvals exist                                 | Approve their own request; widen their own scope; approve their own import or export                                   |
| Space administrator     | Create and delete instances; invite users                         | Space configuration within scope                                                                   | Approve their own governed request. Inherited editor rights do not confer data-use authority                           |
| Agent sponsor           | Create, scope and revoke an agent                                 | Nothing on the agent's output                                                                      | Act as the agent's checker                                                                                             |
| Data controller         | Designate the project's data arrangements                         | Whether a project may access a dataset, and on what terms                                          | Be created by a platform role                                                                                          |
| Data custodian          | Submit dataset intake                                             | Approve, return or reject an import and its named dataset version under the data owner's agreement | Decide their own request; approve on an agent's authority                                                              |
| Data owner or delegate  | Set release conditions for outputs                                | Release authority over output, for a named recipient                                               | Decide their own request, as a delegate                                                                                |
| Checker                 | Nothing on requests                                               | Disclosure decision on staged output                                                               | Be the requester, the agent sponsor, the run principal or any machine identity; release without independent delegation |
| Legal reviewer          | Nothing on requests                                               | Whether approval conditions are met at a checkpoint                                                | Decide their own request; act where conflict rules bar them                                                            |
| Data protection officer | Nothing on requests                                               | Advice, and a recorded position where policy requires                                              | Approve every action automatically                                                                                     |
| Auditor                 | Nothing on requests                                               | Nothing                                                                                            | Edit records; read beyond the authorised scope                                                                         |
| Recipient               | Nothing                                                           | Nothing                                                                                            | Pass a released link to anyone else                                                                                    |
| Agent                   | Submit output, and import requests where policy allows            | Nothing                                                                                            | Approve, check, promote, sign, release or act as custodian                                                             |
| Operator                | Request break-glass access                                        | Pause automated work; a second approval on another person's break-glass request                    | Edit or delete audit records; reach protected data outside break-glass                                                 |

Where one person holds several roles, the matrix applies to each role they hold.

### Operator access and break-glass

Break-glass is the only route for operator access to protected data. It requires a ticket, a second approver who is not the requester, a defined scope and an expiry. The tenant's customer-designated incident or security contact is notified, and the action is recorded. Enhanced (L3) adds time-limited, dual-authorised operator access.&nbsp;

### Effective access

The effective-access view shows who can reach the project, each dataset and each instance, and why. Each reason is explicit, derived from another role, automatic, or approval. An origin that cannot be determined shows as unknown.

### Limits

- A space administrator inherits editor rights on every instance, including read access to snapshots.  
- Auto-assignment creates roster rows from organisation role and space visibility. Each row shows its origin. Derived access is access, not approval.  
- Revoking an organisation role does not remove the space or instance roles that auto-assignment created earlier. In elevated TRE tiers (L1, L2, L3), explicit role discovery is performed on revoke and itemized decisions need to be made.  
- Whether a tenant administrator can read project content depends on effective access. The deployment must evidence it.

## Worked audit trace: one project from request to close-out

This example follows one Controlled project from request to close-out. It uses generic roles. Times are relative to the project's start. It shows the target flow. Today the platform does not record these steps as governance decisions.

| Day and time  | Event                                                                                               | Actor role                           | Record type                      | Outcome                                                          |
| :------------ | :-------------------------------------------------------------------------------------------------- | :----------------------------------- | :------------------------------- | :--------------------------------------------------------------- |
| Day 1, 09:00  | The project owner nominates a project manager                                                       | Project owner                        | Governance assignment            | Pending                                                          |
| Day 1, 10:30  | An independent legal reviewer records approval of the nomination, where policy requires it          | Legal reviewer                       | Decision record                  | Approved                                                         |
| Day 1, 11:00  | The project manager accepts the nomination                                                          | Project manager                      | Governance assignment            | Applied                                                          |
| Day 2, 09:00  | A signatory records the data-access agreement, with its document reference                          | Organisation signatory               | Agreement record                 | Signed; effective from its effective date                        |
| Day 2, 14:00  | A custodian who is not the requester approves the dataset version, under the data owner's agreement | Data custodian                       | Decision record; dataset version | Published as a read-only version                                 |
| Day 3, 09:00  | The project manager invites a researcher; the researcher accepts at 10:00                           | Project manager; researcher          | Audit event                      | Invitation pending until accepted; then applied, origin explicit |
| Day 3, 10:05  | The project manager tries to approve their own access request                                       | Project manager                      | Audit event                      | Refused, self-approval                                           |
| Day 4, 16:00  | The researcher stages an output set and submits it with a frozen manifest                           | Researcher                           | Export request; lifecycle record | Submitted                                                        |
| Day 4, 16:01  | The advisory check runs; one staged file is not on the manifest                                     | Automated check                      | Audit event                      | Coverage gap sent to human review                                |
| Day 5, 09:00  | The checker approves the exact frozen content                                                       | Checker                              | Decision record                  | Approved                                                         |
| Day 5, 09:30  | The data owner authorises release to the named recipient, and a single-use link is issued           | Data owner                           | Decision record; delivery record | Delivered                                                        |
| Day 20, 10:00 | The periodic access review confirms the roster                                                      | Project manager, with the data owner | Audit event                      | Confirmed                                                        |
| Day 40, 10:00 | Close-out is requested, and outputs are resolved                                                    | Project owner                        | Lifecycle record                 | Close-out requested                                              |
| Day 41, 09:00 | Access is revoked, and per-plane disposition is recorded; one backup keeps a residual window        | Data custodian and operator          | Deletion record                  | Closed, with a residual until the backup's expiry                |
| Day 41, 09:30 | The project record closes; the audit trail stays for its retention window                           | Project owner                        | Lifecycle record                 | Closed                                                           |

The audit trail keeps every row. The lifecycle record keeps only the current state, which is closed at the end. Roles and timings vary by deployment.

## SATRE self-assessment

SATRE is a self-assessment specification for an operated research environment. A Nuvolos assessment covers one named deployment. It complements standards such as ISO/IEC 27001\.

SATRE groups its requirements into four core pillars: Information Governance; Computing Technology and Information Security; Data Management; and Supporting Capabilities. An optional fifth pillar covers federated research environments.

### How scoring works

1. Each requirement carries an importance: Mandatory, Recommended or Optional.  
2. Each requirement scores 0 (not met), 1 (sufficient), 2 (satisfied) or N/A.  
3. A capability is met when all its Mandatory requirements score 1 or 2\. A pillar is met when all its capabilities are met.  
4. Nuvolos reports a versioned, evidence-linked evaluation. It does not report a percentage or a badge.  
5. Each filled cell links to dated evidence. A control that cannot be shown with dated evidence scores as a gap.

**Example.** A capability holds one Mandatory requirement scored 0\. That capability is not met, and neither is its pillar. Recommended and Optional scores do not gate a capability.

Mandatory requirements gate any SATRE-compliant claim. The table below states the Mandatory requirements that apply to Controlled (L1), in words. Auditors can match each row to the specification.

### Controlled (L1) against the Mandatory requirements

| Requirement, in words                                                              | Importance | Status and note                                                                                                                                                                |
| :--------------------------------------------------------------------------------- | :--------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No dataset access without the data controller's agreement                          | Mandatory  | Through named project and dataset approval. The platform records the decision but does not create legal authority                                                              |
| Block copy-out through the system clipboard                                        | Mandatory  | Per deployment.                                                                                                                                                                |
| Shared services must not allow cross-project data access                           | Mandatory  | Per deployment. An instance boundary alone does not show it; each deployment demonstrates it                                                                                   |
| Mitigate and record risk from licensed software that contacts an external service  | Mandatory  | Per deployment. The deployment confirms the connection is secure and records its assessment                                                                                    |
| Block outbound internet by default                                                 | Mandatory  | Gap. Network restrictions vary by deployment, and an approved-destination list alone does not block other paths                                                                |
| Maintain and review significant security logs                                      | Mandatory  | Met, two parts. The tamper-evident chain is one part. Storage controls, retained events and review complete the requirement.                                                   |
| A policy on data deletion                                                          | Mandatory  | Per deployment, once retention rules are agreed and every data plane is covered                                                                                                |
| Reasonably prevent unauthorised data in or out                                     | Mandatory  | Met to within reasonable expectation. Listed routes are refused and reviewed. Some interactive channels and analogue paths remain residual risks, these are always enumerated. |
| Specify supported data categories                                                  | Mandatory  | Per deployment, stated against that deployment's security capabilities                                                                                                         |
| Unique accounts, verified identity and least privilege                             | Mandatory  | Partly met. Accounts are unique. On TRE levels,invitation acceptance does verifies the named person. The organisation runs onboarding, verification and review.                |
| Multi-factor authentication for all users                                          | Mandatory  | Via the identity provider. It depends on the deployment's identity configuration                                                                                               |
| Documented disclosure control and an assigned checker responsibility               | Mandatory  | Supported through the output airlock and named checkers                                                                                                                        |
| A policy for outputs that cannot be checked by hand, including trained model files | Mandatory  | Trained model files are the hard case; the default is that they do not leave                                                                                                   |
| Document all features of the implementation                                        | Mandatory  | Supported by this documentation, scoped to the deployment                                                                                                                      |

&nbsp;

Public-involvement requirements 1.7.01 to 1.7.03 are Mandatory for TREs holding personal data. They are mainly the customer's obligations, supported by transparent deployment documentation.

Nuvolos adds two rules that SATRE does not require: at least one independent checker for Controlled, and a checker who differs from the requester. Nuvolos presents them as its own choices. SATRE requires that output-checking responsibility is assigned. It does not require checker independence.

## Shared responsibility

Responsibility is shared, and the deployment agreement sets the split. Each party operates the parts assigned to it.

| Area                           | Nuvolos or designated operator                                      | Organisation, controller or project                                                       |
| :----------------------------- | :------------------------------------------------------------------ | :---------------------------------------------------------------------------------------- |
| Data classification            | Supported storage and controls                                      | Classifies and authorises the data it controls                                            |
| Accounts and identity          | Unique accounts, multi-factor authentication, role model            | Verifies identity, manages membership, reviews access                                     |
| Project and dataset approval   | Workflow and decision record                                        | Decides eligibility, purpose and dataset approval                                         |
| Legal and governance decisions | Gate workflow and decision records                                  | Legal position, signatory authority, review rules and appointments                        |
| Output disclosure control      | Airlock, checks and decision records                                | Policy, checker and release-authority appointments                                        |
| Platform operations            | Assigned components, patching, backups and monitoring               | Any organisation or host components assigned to it                                        |
| Keys and custody               | Custody documentation and supported key model                       | Key choice and, where supported, key holding                                              |
| Data subject requests          | Roster, approval and deletion records that the organisation can use | Responds to data subjects as controller; any support from Nuvolos is set in the agreement |
| Incident response              | Controls, alerts, break-glass, and its own notification duties      | Its own response, and who is notified and within what period                              |
| Self-assessment                | A scoped, evidence-linked assessment                                | Reviews it and decides what assurance to accept                                           |

&nbsp;

For automated work, a named human sponsor is accountable for each agent. Agents run only in Controlled (L1), and only where the deployment has enabled them. Responsibility does not shrink as autonomy grows.

### Data subject requests and notification

The organisation answers data subjects as the controller. Nuvolos provides the records that the organisation draws on, such as the roster, approvals and deletion record. Any support beyond those records is set in the deployment agreement.

Who must be told of an incident, and within what period, comes from the deployment agreement and any legal duty.

### Limits

- Nuvolos does not give legal advice, verify signatures or decide whether processing is lawful.  
- Nuvolos does not decide whether the organisation must notify a regulator or a data subject.

## Incident response

The organisation names the people who own incident response. Nuvolos supplies detection, containment and accountable access.

1. **Detection.** Refusals, failed actions and control events are recorded. Alerts cover audit export failure, enforcement switched off and a stalled review queue.  
2. **Containment.** An operator, or an administrator for their own organisation, can pause automated work for one principal (an account or automated principal), one organisation or the whole deployment. A pause refuses new work. Running work stops only through a separate action.  
3. **Spending limits.** A budget is a financial limit on a resource pool. Whether it stops running work or only reports a balance depends on its type and the deployment. The deployment must state and evidence any enforcement. Stopping running work under an enforced cap is not a pause: a pause refuses new work and does not stop a running step. An agent run allowance is advisory unless the deployment states that it is enforced. A batch allowance may or may not act as a hard cap. Budgets do not reserve capacity.  
4. **Privileged access.** Operators reach protected data only through break-glass.  
5. **Notification.** The agreement and any legal duty set who is told and within what period.  
6. **Learning.** Findings change controls and processes.

Some disclosure paths lie outside what a platform can prevent. These include a photograph of a screen, retyping, and a person with legitimate access who copies what they see. Nuvolos records these as residual risks.

### Limits

- Nuvolos does not claim that a pause halts running work at once.  
- Public reporting of incidents and near misses is a recommended practice. It is not a fixed platform behaviour.

## DPIA and ethics support

The organisation performs and owns any data protection impact assessment. Nuvolos keeps records that the assessment can draw on. Each deployment states which records it provides. Nuvolos does not perform the assessment and does not state its outcome.

| Record                                    | What it supports in the assessment                                       |
| :---------------------------------------- | :----------------------------------------------------------------------- |
| Project purpose and approval decision     | The stated purpose, the eligibility decision and the approvers           |
| Dataset approvals and versions            | Which data, which version, and the conditions attached                   |
| Agreement record                          | Parties, scope, conditions, term and status                              |
| Protection level and plane coverage       | The level, the planes covered, and any combination refused at onboarding |
| Access roster with origin                 | Who can reach what, and why                                              |
| Decision records and receipts             | What left the project, who decided, and what content was reviewed        |
| Deletion record                           | What was removed on each plane, and what remains                         |
| Key-custody map and subprocessor register | Who holds keys, and which vendors and regions apply                      |

For ethics, Nuvolos can hold a reference to an approval the organisation obtained, and link it to the project's decisions. Nuvolos does not give ethics approval. The reference shows that the process took place. It does not show that the research meets ethical standards.

### Limits

- The records show who decided and when. They do not show that processing is lawful.

## Public and gated evidence

Nuvolos separates public explanation from gated evidence. The public area describes controls, scope and responsibilities in plain language. The gated evidence is an organisation-specific pack, released under the organisation's agreement.

The pack contains the self-assessment, the key-custody map, decision records and audit-trail exports. Every document states its scope, version and date. Organisations can request the evidence their due-diligence process needs.

## What Nuvolos does not claim

- **No tamper-proof audit.** The trail is tamper-evident and unsigned.  
- **No operator blindness.** Operator access is accountable and time-limited.  
- **No air gap.** Locked (L2) and Enhanced (L3) restrict network access but are not an air gap.  
- **No outbound-internet block in Controlled by default.** Controlled does not yet meet every Mandatory SATRE requirement, and outbound internet is not blocked by default. Block levels may be increased granularly to SATRE requirement levels inside Controlled on a per-deployment basis.  
- **No control over external model providers.** An external model call discloses its content. Nuvolos cannot control what the provider does with it. Without an agreement, its retention and training use is unknown.  
- **No session control over pixels.** Clipboard and transfer controls do not stop screenshots, photographs or retyping.  
- **No universal residency or fixed retention.** Both are per-deployment commitments.  
- **No service-level or turnaround guarantee,** unless the organisation agrees one and it is measured.  
- **No "fully erased" claim** while a residual data plane remains.  
- **No cryptographic proof of release** while receipts are unsigned.  
- **No automatic authority** from a platform role, creator label or administrator role.  
- **No auto-approval.** Missing approvals, empty reviewer lists, unavailable reviewers and expired decisions hold or close the action.  
- **No signature service** and no power to bind the organisation.