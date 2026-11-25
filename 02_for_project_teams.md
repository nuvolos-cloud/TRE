# For Project Teams

This document is for people who run a Nuvolos project day to day. They include project owners, project managers, data custodians, output checkers and workspace and permissions operators. It describes the TRE experience.

## Roles in a project

Your organisation assigns governance duties. It grants platform capabilities separately, each within a defined scope. One person can hold several roles where the separation rules permit. A job title alone grants no capability and no access to data.

| Role                              | What you do                                                                                                                                                        | What you cannot do                                                                                                                                                                                                                    |
| :-------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Project owner                     | Set the project's purpose, terms and funding. Nominate the project manager. Own the expected outputs.                                                              | Sign for your organisation unless it gives you that authority. Approve your own access or exports.                                                                                                                                    |
| Project manager                   | Coordinate the project and request changes. Invite people or manage roles only with separately delegated capabilities.                                             | Read project data because you manage it. Approve your own requests or widen your own scope.                                                                                                                                           |
| Data custodian                    | Run dataset intake. Approve, return or reject each import under the data owner's agreement.                                                                        | Decide an import you requested. Gain researcher access to an instance by custody alone.                                                                                                                                               |
| Data owner or delegate            | Hold release authority for outputs under the data agreement.                                                                                                       | Act beyond the terms of the data agreement. Decide dataset access or set conditions. The data controller agrees access, and the asset owner sets conditions.                                                                          |
| Researcher                        | Work in an instance at Controlled (L1). Submit results for review.                                                                                                 | Release results. Approve datasets. At Locked (L2) or Enhanced (L3), use an interactive researcher session.                                                                                                                            |
| Output checker                    | Decide whether to approve, return or reject each staged output.                                                                                                    | Check your own request, or an output from an agent you sponsor. Release an output on your own authority. At Controlled (L1), only separately delegated checkers can release. At Locked (L2) or Enhanced (L3), no checker can release. |
| Agent sponsor                     | Create and revoke an agent, and be accountable for what it does.                                                                                                   | Check the output of an agent you sponsor.                                                                                                                                                                                             |
| Workspace or permissions operator | Create empty instances (workspace operator), or administer invitations and delegated role changes (permissions operator), when separately granted that capability. | Gain editor access, decide data use, grant yourself access or exceed delegated authority. Operating the project grants none of these.                                                                                                 |

&nbsp;

Nuvolos records these assignments and changes to assignment status. It does not create legal authority. The Owner label is display metadata, derived from the space creator. It is not a governance role. In TRE levels (L1,L2,L3), creating a space does not grant the creator space-wide editor access. The ordinary product's broad space-administrator role is an L0-only catch-all role.

**Break-glass** is the accountable route for infrastructure-operator access to project data. It needs a ticket, a second approver, a defined scope and an expiry. Your tenant is notified, and the access is recorded.

## TRE permissions matrix

A named capability must be granted for the relevant scope. A governance title alone is not a grant. A manager can hold separately delegated capabilities. Doing so does not make them an ordinary space administrator or give them data access. The adopted profile's combination rules apply. Required independent decisions, identity binding, acceptance and dataset approvals still apply. In this matrix, the technical administrator is the bounded technical-administration bundle. It creates empty instances as the workspace operator in the setup steps. It is not the ordinary product's (L0) broad space administrator.

| Action                  | Responsible capability or assignment                                                                                                 | Boundary                                                                                                                                                                                                                   |
| :---------------------- | :----------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create an instance      | Workspace lifecycle, exercised by the technical administrator. A manager may hold it only where the profile permits the combination. | Creates an empty instance. It grants no automatic editor or data access. L3 separates technical administration from the project manager.                                                                                   |
| Invite people           | Membership administration. A project manager may hold it if delegated.                                                               | Invitations are scoped and bound to an identity. Sending one is not a grant.                                                                                                                                               |
| Change instance roles   | Membership administration, for the delegated grant types and instance.                                                               | Required independent approvals and acceptance come before a grant. No one can self-grant or self-escalate. A proposed L3 widening grant needs a second authorisation.                                                      |
| Start applications      | A separately authorised research or data-use capability, plus instance editor access at Controlled (L1).                             | Administration does not confer content access. In L2 and L3 mode, researchers use batch jobs, not interactive sessions.                                                                                                    |
| Request import          | An eligible project participant, within their authorised request scope.                                                              | The requester cannot approve their own import.                                                                                                                                                                             |
| Approve import          | An independently authorised destination custodian or delegate.                                                                       | Source export and destination import decisions are separate. Both are bound to a version. At L2, data-owner approval is required new datasets. At L3, custodian and data-owner decisions are separate.                     |
| Submit output           | An authorised researcher, or another eligible requester.                                                                             | At L1, outputs use the approved working path. In L2 and L3 mode, batch outputs are staged for review. Submitting does not release an output.                                                                               |
| Check output            | An assigned, qualified independent checker.                                                                                          | A checker cannot review their own request or an agent output they sponsor. L1 needs one checker. L2 and L3 mode needs two independent checkers, and both must approve.                                                     |
| Authorise release       | The data owner or an authorised delegate.                                                                                            | Checker assignment alone gives no release authority. At L1, a separately delegated, eligible checker may release. L2 and L3 policy requires a release authoriser who is neither checker. The recipient must be authorised. |
| Change protection level | An authorised project request and policy decision.                                                                                   | A reduction needs a new space at the lower protection level, plus a governed migration. There is no in-place downgrade.                                                                                                    |
| Enable resources        | Scoped resource administration within the approved envelope. A manager may hold it only where the profile permits.                   | Funding and pool mapping need their own authority. Resource changes grant no data access. L3 separates technical administration from the project manager.                                                                  |
| View effective access   | A scoped assurance or roster-view capability. A manager may hold it if delegated.                                                    | Shows origins and residual access. It grants no access to project content.                                                                                                                                                 |
| Close project           | An authorised close-out executor, after the project owner's and data owner's disposition decisions.                                  | The executor and the requester cannot approve their own deletion. L3 policy adds a second authorisation. Revocation and per-plane disposition follow policy.                                                               |

&nbsp;

Three notes apply to the role matrix:

- At Locked (L2) or Enhanced (L3), researchers have no interactive instance role. They submit batch jobs against approved data.  
- In the ordinary product (L0), a space administrator inherits editor rights on every instance. TRE level’s no-data administration bundle does not do this.  
- Effective-access visibility has its own scope. The holder needs the right roster or assurance capability, not the legacy space-administrator role.

## Set up a project

Follow this fixed order to set up a project. Protected work starts only after the required approvals are recorded.

1. **Request the project.** The project owner states the purpose, datasets, protection level and the people involved.  
2. **Record the approvals.** The data controller or an authorised delegate agrees to dataset access. The asset owner, meaning the information asset owner, sets the dataset's conditions. The asset owner is not necessarily the data owner, who holds release authority. Your organisation's legal or ethics review applies where its policy requires one.  
3. **Create the space.** An authorised person creates a protected project space at the chosen protection level. Creating the space gives that person no project-data access and no governance assignment.  
4. **Create instances.** Create one instance per person for individual work. Create a shared instance for approved people who work on the same data.  
5. **Invite people and map roles.** A person with delegated membership capability sends each identity-bound invitation. Access starts only after acceptance and all required decisions. The grant's expiry is recorded separately.  
6. **Assign checkers.** Assign qualified, independent checkers for each output path. Controlled (L1) needs at least one. Locked (L2) or Enhanced (L3) needs two.  
7. **Enable resources.** Establish the budget mapping and enable the sizes and GPU resources the project needs.  
8. **Verify access.** Open the effective-access view and compare it with the approvals. Fix any gap before anyone uses protected data.

Nuvolos records these decisions. It does not create legal authority for them.

### Choose per-person or shared instances

A per-person instance suits one researcher's individual analysis. A shared instance suits several approved people who work on the same data. Each editor signs in with their own login.

| Pattern             | Use it when                                   | Created by                                             | Who holds the editor role                  |
| :------------------ | :-------------------------------------------- | :----------------------------------------------------- | :----------------------------------------- |
| Per-person instance | One researcher needs their own analysis       | Workspace lifecycle capability, for a named researcher | That researcher, after required approval   |
| Shared instance     | Several approved people work on the same data | Workspace lifecycle capability                         | Each approved person, with their own login |

Keep one protected space per project. Use separate project spaces where the permitted data differs between people. An instance organises work. It is not a separate security boundary.

### Invite people and map roles

An authorised membership operator (the permissions operator in the roles table) invites people. An authorised workspace operator creates instances. A manager may hold either capability if delegated. Holding it gives no data access. An invitation is not a grant. The intended person must accept, and all required project and dataset decisions must be in place.

| Person                                     | Role to give                                                                                            | Note                                                                                      |
| :----------------------------------------- | :------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------- |
| Researcher at Controlled (L1)              | Instance editor, in their own or a shared instance                                                      | Only editors run applications and change files.                                           |
| Researcher at Locked (L2) or Enhanced (L3) | No interactive instance role                                                                            | Submit batch jobs instead.                                                                |
| Data custodian                             | Dataset-space permissions and import decision rights, only as needed                                    | Custody does not grant researcher access.                                                 |
| Output checker                             | Review path only                                                                                        | At Locked or Enhanced, the checker uses a contained reviewer session.                     |
| Project manager                            | Project coordination, plus only the separately delegated membership, lifecycle or resource capabilities | Management gives no instance-data access. Any researcher access is separately authorised. |

To invite a researcher to a per-person instance:

1. An authorised workspace operator creates the empty instance for the named researcher.  
2. An authorised membership operator sends an identity-bound editor invitation. The invitation has its own expiry. The grant's scope and expiry are recorded separately.  
3. The named researcher accepts. The required project and dataset decisions are confirmed independently.  
4. An authorised person checks the effective-access view. They confirm the active editor grant, its origin, scope and conditions.

### Invitation lifecycle

An invitation moves through the states below. Only the grant active state gives access.

| State        | Meaning                                                                                                                                               | Next states                    |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------- |
| Created      | The invitation exists with its role, validity and maximum number of accepts. It has not been sent.                                                    | Sent, Send failed              |
| Sent         | The invitation reached the recipient. It is not a grant.                                                                                              | Accepting, Revoked, Expired    |
| Send failed  | The invitation did not reach the recipient. It grants nothing.                                                                                        | None. Create a new invitation. |
| Accepting    | Each acceptance is recorded in a response row, up to the maximum number of accepts.                                                                   | Grant active, Revoked, Expired |
| Grant active | The named recipient accepted. All required decisions and grant conditions are in place. The origin shows as explicit.                                 | Revoked, Expired               |
| Expired      | The invitation expiry stops further acceptance. A grant expires separately, at its recorded end time.                                                 | None                           |
| Revoked      | An authorised membership operator revoked the invitation or grant, and recorded a reason. Revoking an invitation alone does not undo an active grant. | None                           |

Revoking an instance role stops that person's running applications. It also schedules cleanup of their home folder.

A researcher can request a role, then track or withdraw a pending request. Who reviews a request depends on its path. The requester cannot approve their own request.

### Limits

- In the ordinary product, invitation acceptance warns on an email mismatch. It does not refuse the acceptance. TRE levels bind acceptance to the named identity.&nbsp;

## Run the project day to day

### Review access

Review access at the intervals your policy sets. The effective-access view shows who can reach the project, each dataset and each instance. It shows the origin of each grant.

| Origin    | What it means                                                                 | How you act on it                                                                                                          |
| :-------- | :---------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| Explicit  | A direct grant to the person on an instance or space                          | Change or revoke it on the member list.                                                                                    |
| Derived   | Access that follows from another permitted assignment                         | Review and change its source. A protected TRE does not derive editor access from administration alone.                     |
| Automatic | Access created by a permitted automatic assignment                            | Check its source and resulting effect. Protected spaces do not create broad administrator or content grants automatically. |
| Approval  | A recorded project or dataset decision required for a separately scoped grant | Confirm the decision still stands. Approval alone is not a platform grant.                                                 |
| Unknown   | The platform cannot compute the origin                                        | Investigate before you sign off the review.                                                                                |

Follow this procedure for each review:

1. Open the effective-access view for the project.  
2. Review administrative capabilities and every separate content grant. An administrative assignment does not itself count as instance editor.  
3. Read the origin of each row. Check derived and automatic rows closely, because reviewers often miss them.  
4. Confirm that each person still needs their access. Change or revoke it at its source.  
5. After each revocation, reopen the view and check dependent and independent grants, application sessions and credentials; record any remaining access and its basis.  
6. Check that dependent applications and sessions have stopped or been invalidated where required; account separately for any independent grant that remains.  
7. Record the outcome for each person as confirmed, narrowed or allowed to expire.  
8. If you cannot confirm that access has ended, report it as an incident.

In L0, space member list shows direct members and their instance roles. The instance view adds inherited rows. The two can disagree. Membership history shows who created each space or instance, when each person joined, and who invited them. TRE effective-access view reconciles origins. Neither list is complete on its own.

### Limits

- The review is only as complete as the view. Where Nuvolos cannot compute an origin, it shows the row as unknown rather than guessing.

## Resources and budgets

Budgets are financial limits. The platform has balances, gates and refusal behaviour. By default, reached budget limits stop running work and refuses new work, with appropriate prior warnings in place. An allowance shown to a project is a hard limit on pay-as-you-go type costs. A budget does not reserve capacity. 

Accounts and wallets hold the budgets, accounts are cost centres, wallets are specialised resource budgets within accounts. Resources mapped to an account/wallet charge their usage against them. A project is not a budget object. It draws on the accounts/wallets mapped to its space.

| Role                    | Can do                                                                                                                                                       | Cannot do                                                                                                 |
| :---------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| Account/wallet manager  | Set budgets. Enable or disable approved computer sizes for the pool. Transfer credits between eligible accounts/wallets they manage. Link resource accounts. | Change a project mapping alone, without project-side authority. Read protected data because they fund it. |
| Resource manager        | Enable approved elastic sizes and GPU resources. Manage quotas within the project's authorised envelope.                                                     | Change cluster placement, capacity or security boundaries, or gain project-data access.                   |
| Project manager         | Request resource and quota changes. Apply changes within the envelope only with separately delegated resource capability.                                    | Approve their own request.                                                                                |
| Project owner           | Propose the resource envelope and funding route.                                                                                                             | Approve their own governed requests.                                                                      |
| Instance editor         | Use enabled sizes. In research spaces, change an application's size within the included range.                                                               | Enable sizes or GPU resources for the space.                                                              |
| Infrastructure operator | Provision capacity and change clusters, node pools and dedicated placement, as the agreement assigns.                                                        | Read protected data outside break-glass.                                                                  |

The mapping rules are these:

- A resource type cannot be split across multiple accounts/wallets inside one space.  
- A resource type is mapped space by space. It is not mapped for the whole organisation.  
- A mapping is not retroactive. Historical usage is not moved to a new account/wallet.  
- Mapping a space to an account/wallet needs two authorised decisions: a project-side decision for resources, and a pool-side decision for funding. One person may hold both only where separation rules permit (L0).

Sizes work as follows:

- A person with scoped resource-administration capability enables credit-based sizes for the space before editors use them.  
- A size change takes effect when the application restarts.

### Example: enable a GPU size for a project space

1. The account/wallet manager confirms that a node pool providing GPUs is enabled for the pool. The pool configuration refuses, at start, any run it does not permit.  
2. The budget is mapped after the authorised project-side resource and account-side funding decisions.  
3. A person with delegated resource-administration capability enables the approved GPU size for the space.  
4. An editor selects the GPU size and starts an application. The run is charged while it runs.  
5. Check the resource monitoring view. It should show the usage against the budget.

Enabling a resource never widens anyone's data access.

### Limits

- Cost controls are not access controls. Enabling resources changes what can run and what can be spent. It does not change who can see which data.  
- You cannot provision new capacity or change cluster placement yourself. The authorised infrastructure operator does this.

## Change a project's level

Open (L0) is ordinary Nuvolos and is not a trusted research environment. A project moves to a higher level through re-approval. A project moves to a lower level only through a new space.

| Direction                                           | What happens                                                                                                                             | Who acts                                                                                                                                                  |
| :-------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Up, for example from Controlled (L1) to Locked (L2) | Affected approvals are reviewed again. Access and data are re-attested. The new level applies to every instance, workload and data path. | The project owner requests. The data controller and asset owner re-approve within their authority. At L3, the infrastructure operator confirms placement. |
| Down                                                | The level never goes down in place. A new space at the lower level receives only approved material, moved through the airlocks.          | The project owner requests. Each item moves under its own approval.                                                                                       |

To move a project up:

1. The project owner requests the higher level and states the purpose.  
2. Identify every approval that the change affects. Material changes trigger review.  
3. The data controller or asset owner reviews each affected approval again.  
4. Re-attest the project's access and data.  
5. The customer records the required security decision. At L3, the infrastructure operator also records its placement confirmation. That confirms placement readiness, not legal authority. The exact security role is an open deployment-policy choice.  
6. The new level applies to every instance, workload and data path in the space.  
7. Review access against the new level. At Locked (L2), researchers have no interactive researcher session and submit batch jobs.

To move material down:

1. Create a new space at the lower level.  
2. List the approved material to move.  
3. Export each item through the output airlock of the source space, and import it through the import airlock of the new space.  
4. Close out the old space when its material is resolved.

### Limits

- Nuvolos does not lower a level in place. A downgrade always needs a new space and a governed migration.

## As a data custodian: approve an import

You approve, return or reject each import request. Checks assist your decision, but you make it. You cannot decide a request you made, and no agent or machine identity can decide one.

### What you see in quarantine

Each request arrives in quarantine. Quarantine is a per-request area that no project workload can read, mount or execute. Nothing in quarantine is visible to the project's instances.

| Item              | What it shows                                                                                                                                                 |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request           | What is being brought in, where it comes from, why the project needs it, the intended use, any licence or terms, and the dataset name and version it becomes. |
| Quarantined bytes | The staged files, held where project compute cannot reach them.                                                                                               |
| Check results     | Each configured check, its outcome, and any item it could not inspect.                                                                                        |
| Status labels     | "Not scanned", "not covered" or "check not performed". A missing check never appears as a pass.                                                               |
| Requester         | The person who submitted the request. You cannot decide a request you submitted.                                                                              |

Configured checks can include malware and security scanning, format and integrity checks, metadata or disclosure pre-screening, and licence and category tagging. Each result is recorded against the request.

A required check that fails or cannot run blocks promotion. The request is held with a reason. No approval path exists around it. If a check is not configured or does not support the item, the material proceeds only where the intake policy permits that case. An authorised person other than the requester must then record a risk decision. Otherwise, the material stays in quarantine or is rejected.

### Decide the request

1. Open the request in quarantine.  
2. Read the request. Confirm the purpose, the terms and the version name.  
3. For data from outside Nuvolos, confirm that the source's own release procedure is recorded in the request. If it is not, refuse.  
4. Read each check result. Note every item marked "check not performed" or "not covered".  
5. If the intake policy allows an uncovered case, decide whether to record the risk decision yourself. You must not be the requester.  
6. Confirm that the version name is new.  
7. At Locked (L2), confirm that the data owner has approved any new dataset. At Enhanced (L3), confirm that a separate data-owner decision is recorded. Step 7 reflects the proposed profile policy.  
8. Decide, and record your reasons.

| Decision                  | Effect                                                               |
| :------------------------ | :------------------------------------------------------------------- |
| Approve                   | Publishes the named read-only version for the project.               |
| Return for changes        | Keeps the request unpublished. The requester fixes it and resubmits. |
| Reject                    | Closes the request with reasons. The quarantine record is kept.      |
| Withdraw (requester only) | Closes the request. Nothing is published.                            |

Your authority comes from the data owner's agreement, not from a platform role. If you are not the data owner, you must be a named delegate with a recorded scope.

### Versions

- Name each approved version. Nuvolos refuses publication as an existing version, so every import creates a new version.  
- The version record binds file bytes to checksums. It binds table data to an immutable version identifier. It also records the source, request, approver, decision and date.  
- A version never changes. Correcting or extending data needs a new version and a new decision.  
- Project workloads read an approved version through a read-only mount or a versioned query path.  
- Your deployment's policy decides whether a superseded version is retired or kept. Nuvolos does not silently re-point a superseded version.  
- Any change to the source bytes, the version or the terms after approval invalidates the approval. The material returns to the request stage.

### Limits

- The intake record is a starting point for provenance. Nuvolos does not track every later transformation of the data  automatically.  
- A check that was not configured, or that cannot inspect the item, is never counted as a pass.  
- Nuvolos does not create your authority. The data owner's agreement provides it.

## As an output checker

You decide whether an output may leave the project. Independence is a hard requirement. You decide only the exact bytes in front of you. You decide each output on its own frozen manifest.

### Independence and assignment

A separately authorised assigner assigns checkers and runs the queue, and cannot name themselves as a checker. Assignment never gives release authority. It also does not make an ineligible person eligible.

You cannot check an output if you are the requester, the run principal (the identity the run executes as), the agent principal (the agent's own identity), the agent's sponsor, or a service or machine identity. Nuvolos enforces these exclusions and records any refused attempt.

If you have a conflict of interest, declare it. Step aside where your organisation's rules require it. Nuvolos records who decided. It does not decide whether a conflict exists.

### What the checker screen shows

| Panel              | What it gives you                                                    | How to use it                                      |
| :----------------- | :------------------------------------------------------------------- | :------------------------------------------------- |
| Frozen manifest    | Every staged item with its checksum, written once at submission      | Confirm that the manifest lists everything staged. |
| Check results      | Disclosure checks run against the manifest, with each check's status | Read them as advisory evidence only.               |
| Release comparison | Earlier releases from the same project                               | Look for differencing across releases.             |
| Staged content     | The exact bytes listed in the manifest                               | Review them against the disclosure policy.         |

### Checking steps

1. Confirm that the manifest lists everything staged. An item that is not listed is a coverage gap. It goes to human review and is never released.  
2. Read the check results as evidence. "Check not performed" is never a pass. A check that cannot complete reaches you with that status shown.  
3. Review the content against the project's disclosure policy. For code and notebooks, also look for embedded data and credentials.  
4. Compare the output with earlier releases. Several releases together can reveal values that each release suppresses alone.  
5. Treat trained models with care. They are not released by default. They leave only where the agreed policy affirmatively allows it.  
6. If you cannot inspect an output meaningfully, and the policy does not permit its release, the output stays inside the project.  
7. Decide, and record your reasons.

### Decisions and reasons

| Decision           | Effect on the request                                       | Effect on release                                     |
| :----------------- | :---------------------------------------------------------- | :---------------------------------------------------- |
| Approve            | The exact frozen content may go to an authorised recipient. | Release may proceed under the data owner's authority. |
| Return for changes | The request goes back to the requester with reasons.        | Nothing is released.                                  |
| Reject             | The request closes with reasons. The record is kept.        | Nothing is released.                                  |

Record reasons for every return and every rejection. Requesters see them. A refused export route also gives a reason and opens a submission prefilled with the refused items. Nuvolos records both the refusal and the submission.

### Controlled (L1) compared with Locked (L2) and Enhanced (L3)

|                      | Controlled (L1)                                                                         | Locked (L2) and Enhanced (L3)                                                         |
| :------------------- | :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| Checkers needed      | At least one qualified, independent checker                                             | At least two qualified, independent checkers, both approving                          |
| Your environment     | An ordinary project session under your own platform identity                            | Contained reviewer session. You inspect the content and cannot download it.           |
| Session controls     | Screen-only streaming, with the controls described under Session controls at Controlled | The same, with paste-in also blocked                                                  |
| If checkers disagree | Not applicable. One checker decides.                                                    | Nothing is released until both are satisfied, or the request is returned or rejected. |
| Release authority    | Data owner or delegate, or an independently delegated eligible checker                  | Data owner or authorised delegate, who is neither checker for that output             |

### Two checkers at Locked (L2) or Enhanced (L3)

Locked or Enhanced needs two checkers, and both must approve. A single approval releases nothing.

1. Each checker reviews the frozen manifest and decides.  
2. If both approve, the output moves to the data owner or delegate for release.  
3. If the checkers disagree, nothing is released. The request is returned for changes, or it is rejected. It can also wait until both checkers are satisfied.

### Release and delivery

- Release needs the data owner's authority. At Controlled (L1), an eligible checker can release only if the owner has delegated that authority to them. At Locked (L2) and Enhanced (L3), neither checker can release. Otherwise, the data owner or a delegate authorises release after the check.  
- Approved content goes only to an identity-bound, expiring, single-use link for an authorised recipient. Nuvolos issues no link to anyone else.  
- Any change to the bytes after approval invalidates the approval. The new content goes through checks and review again.  
- If a transfer fails or is interrupted, Nuvolos records it as not delivered. Partial bytes may already have reached the recipient. Reissuing the link is a new governed action for the same content and the same recipient.  
- A retrieval record does not prove that a recipient deleted later copies.

### Limits

- At Controlled (L1), the checker works in an ordinary project session behind the remote desktop, not in a contained reviewer session.  
- Nuvolos does not promise automated differencing checks. Your review covers differencing across releases.  
- Trained models are not released by default. The agreed policy must affirmatively allow their release.  
- Nuvolos measures waiting times and shows them. It does not promise a turnaround time.

## Session controls at Controlled (L1)

At Controlled (L1), each interactive app runs in its own container. A remote-desktop sidecar renders the app and streams its screen to the user's browser. The sidecar is a named, owned, unprivileged component in the same workload. It runs the app in an isolated browser or desktop session.

The app listens only inside the workload. The sidecar is the only part of the workload that can be reached. The direct address of the app is not exposed.

| Control                                                    | Default                                                                                           |
| :--------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| Copy-out from the application session to the user's device | Blocked. This cannot be changed.                                                                  |
| Paste-in, into the session                                 | Allowed up to a size limit. Every attempt is logged. Project policy can block, limit or allow it. |
| File transfer, in either direction                         | Blocked. Files move only through the import and output airlocks.                                  |
| Downloads and printing from the in-session browser         | Disabled                                                                                          |
| Direct address of the app                                  | Not exposed                                                                                       |

On covered channels, clipboard and transfer attempts are logged with direction, size and outcome, never content.

At Locked (L2) or Enhanced (L3), the contained reviewer session uses the same sidecar. Paste-in is also blocked there. Output checkers inspect the staged content in that session. The governed route for output to leave is release through the output airlock.

### Limits

- The sidecar controls clipboard and transfers on covered channels. It does not control pixels. Screenshots, screen recording, photographs, retyping and on-device text recognition remain possible.  
- Streaming adds latency to interactive work.  
- Paste-in brings data into the project.  
- An app that cannot run behind the sidecar is not offered at Controlled (L1), unless an exception is recorded on the deployment's verdict page.  
- Nuvolos does not block outbound internet by default at Controlled (L1).

## Handle refusals and escalations

Where the deployment's evidence confirms it, Nuvolos refuses these routes: file download, download links, legacy public token routes (bearer-token download URLs that do not require a signed-in recipient), snapshot download, application export, image export, publish or distribute, and agent output promotion. Check each route, including publish or distribute, against that deployment's evidence. The legacy token route is not the identity-bound airlock delivery link. Each refusal gives a reason. It also opens a submission prefilled with the refused items. Nuvolos records both the refusal and the submission.

Use this table when a request stops moving:

| Situation                     | What happens                                                                      | What you do                                                                 |
| :---------------------------- | :-------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| A checker is unavailable      | The request waits or escalates under policy. The output stays inside the project. | Assign another checker or escalate.                                         |
| A request is overdue          | It escalates or expires. Nothing is released automatically.                       | Escalate. Timeouts never release content.                                   |
| A check did not run           | The request shows "check not performed".                                          | Retry the check, supply an alternative, or decide with that status visible. |
| A delivery fails              | Nuvolos records it as not delivered.                                              | Reissue the link through the governed flow.                                 |
| A recipient is not authorised | No link is issued.                                                                | Confirm the recipient's authority under the data owner's policy.            |

## Close out a project

Close-out ends access, disposes of each data plane under policy, and records what remains. Nuvolos never reports data as fully erased while a copy remains.

1. **Stop new work.** The project stops accepting new work under its end-of-life process.  
2. **Resolve outputs.** Submit anything the project still needs to release through the output airlock. Nothing bypasses it.  
3. **Revoke access.** Revoke access for everyone, including credentials. Stop running applications, batch jobs and agent runs. Revoking access does not stop batch jobs by itself, so confirm that each stop has been observed. Reopen the effective-access view and confirm that no rows remain. If you cannot confirm this, report an incident.  
4. **Dispose of each data plane.** Record the disposition of each plane as shown below.  
5. **Handle external copies.** Where the organisation owns the external store or its keys, deletion of that copy is the organisation's action. State this in the record.  
6. **Collect evidence.** Gather the decision records, the disposition of each plane and the residual windows.  
7. **Delete the space.** An authorised close-out executor deletes the space after the required independent disposition and deletion decisions.

| Data plane                                                 | What to record                                                        | Residual                                                |
| :--------------------------------------------------------- | :-------------------------------------------------------------------- | :------------------------------------------------------ |
| Instance files (Workspace, Personal and Application areas) | Deleted, archived or retained                                         | \-                                                      |
| Tables                                                     | Deleted or retained, covering both the metadata and the table backend | Residual until the date recorded for the backend.       |
| Bulk storage shares                                        | Share disposition                                                     | Residual until the date recorded.                       |
| Snapshots                                                  | Deleted or retained                                                   | Residual until the date recorded.                       |
| Backups                                                    | Retention window                                                      | Residual until the date recorded at close-out.          |
| External-store registrations                               | Registration removed. The external copy is the organisation's.        | The organisation-held copy is outside platform control. |

Retention periods come from your deployment's policy and data agreements. Nuvolos does not invent them.

The record is evidence of process. Collect the decision records and the residual windows together. The audit trail can be exported to your own SIEM. It covers only events recorded since capture started, and it cannot rebuild earlier history.

### Limits

- Deleting a visible file does not prove that every copy is gone. Backups and provider-side copies persist until their documented expiry.  
- A file that disappears from the project view is not proof of deletion.

## A worked example: a university organisation

A university can use one organisation for its trusted research work. This works only if the institution can show that effective administrator access, derived and automatic rights included, is safe. It must also show that the data planes and the policy are safe. An organisation boundary alone does not prove a dedicated cluster. Otherwise, use separate organisations along real legal or operational boundaries.

The example below uses only generic roles and generic values.

- **Dataset spaces.** Each dataset sits in its own private dataset space, with the asset owner's conditions recorded. A named custodian manages it. Researchers hold no role there.  
- **Project spaces.** Each research project sits in its own protected space. The project owner signs only if the university has authorised them to do so. The owner then nominates a project manager.  
- **Manager access.** The project manager coordinates without data access. Membership, workspace or resource capabilities are separately delegated as needed; any researcher access requires its own approval.  
- **Data into a project.** The custodian approves a named version. Moving data from another space needs an export decision in the source space and a separate import decision in the project. A viewer role is not a transfer.  
- **Researchers.** Each Controlled (L1) researcher gets a per-person instance as editor. Approved collaborators share an instance.  
- **Checkers.** Named, qualified checkers who are not on the project review outputs. Controlled (L1) needs one. Locked (L2) or Enhanced (L3) needs two.  
- **Budget.** A resource-pool manager allocates the project's budget. The budget is a financial limit; whether reaching it stops running work or refuses new work depends on the deployment's configuration and the resource type.  
- **Reviews and close-out.** Access is reviewed at the intervals your policy sets. The project is closed out one data plane at a time.

### Setup sequence

1. Create a private dataset space for each dataset. Record the asset owner's conditions. Assign a named custodian. Give researchers no role in that space.  
2. Record the data controller's agreement and the asset owner's conditions for each dataset. Record the signatory's authority.  
3. Import each dataset as a named version through the import airlock. The custodian approves the version.  
4. Confirm that the project owner holds the institution's authority to sign, or name a signatory who does.  
5. Record the project request: purpose, people, datasets and protection level. Protected work waits for these approvals.  
6. An authorised person creates a protected project space without automatic project-data access.  
7. Nominate the project manager and separately grant only the required scoped capabilities after any required approvals and acceptance.  
8. Create one per-person instance for each Controlled (L1) researcher. Create a shared instance for approved collaborators.  
9. Send each invitation with its editor role and an expiry. Confirm each acceptance.  
10. Assign at least one named, qualified checker who is not on the project. At Locked (L2) or Enhanced (L3), assign two.  
11. Enable the sizes and GPU resources the project needs. Authorised project-side and pool-side decisions establish the budget mapping.  
12. Open the effective-access view and compare it with the approvals. Fix any gap before work starts.  
13. Set the review interval in your policy. Start work.

## Limits

- Role labels are not confidentiality guarantees. Check effective access and route enforcement; do not rely on the viewer or observer role as a read barrier without deployment evidence.  
- At L0, a space administrator can read, change and act across all instances. TRE levels replace this default with separately authorised bounded capabilities.  
- Whether organisation managers can read project instances depends on effective access. Check the effective-access view for your organisation.  
- At Controlled (L1), the checker works in an ordinary project session behind the remote desktop, not in a contained reviewer session.  
- At L0, invitation acceptance warns on a named-email mismatch rather than refusing it. TRE levels require identity-bound acceptance.  
- At L0, revoking an organisation role does not remove space or instance roles it created automatically earlier. At TRE levels, the platform explicitly requires decisions on each sub-role.  
- Personal areas are not captured in snapshots. Check coverage and restore behaviour for the deployment. Shared-mode home folders are shared across authorized users.
- Infrastructure operators can technically reach project data. Every such access runs as break-glass. It needs a ticket, a second approver, a scope and an expiry. Your tenant receives a notification.  
- The audit trail is tamper-evident, not tamper-proof. Decision receipts are recorded but unsigned. The trail covers only events recorded since capture started.  
- Platform roles do not create legal authority. Your organisation's agreements provide it.  
- TRE levels enforce the project manager's separately granted capabilities and scope on the server. Platform authorisation checks enforce them, not user-interface restrictions alone.&nbsp;