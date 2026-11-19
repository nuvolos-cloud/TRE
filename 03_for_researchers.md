# For Researchers

This document is for analysts and data scientists who do research in a Nuvolos Trusted Research Environment (TRE). It explains how your project works, how you bring data in, how you run analysis, and how results leave. Each TRE project runs at Controlled (L1), Locked (L2) or Enhanced (L3), and Open (L0) is ordinary Nuvolos, which is not a TRE.&nbsp;

### Your project in 60 seconds

Your project is one space. Its protection level applies to every instance, application and data path in it. An instance is a work area inside the space that holds files and applications. It is not a separate security boundary. Ordinary Nuvolos lets you download files, create download links, export applications and publish content. Controlled (L1), Locked (L2) and Enhanced (L3) projects do not offer those routes directly.

Five things differ from ordinary Nuvolos:

1. Data arrives through an import request. A custodian who is not the requester runs intake and approves each dataset version, under the data owner's agreement.  
2. You work with applications from an approved catalogue, at approved versions.  
3. Results leave only through the output airlock, after human review.  
4. In Locked and Enhanced, you submit batch jobs instead of opening interactive sessions. The work has no internet access.  
5. AI use is restricted. Agents run only in Controlled, and each one has a named human sponsor.

In this document, a session means one running application, not a login to Nuvolos.

A project never moves to a lower level in place. Moving to a higher level needs re-approval. If work needs less protection, the approved material moves to a new space through the output airlock.

## Which level you are in

Your level decides which tools, sessions, connections and AI services you can use. If you are not sure which level applies, ask your project manager. The table compares the levels on the points you meet most often.

|  | Controlled (L1) | Locked (L2) | Enhanced (L3) |
| :---- | :---- | :---- | :---- |
| Sessions | Interactive applications from the catalogue, behind the remote-desktop sidecar | No interactive sessions; batch jobs only | Same as Locked (L2) |
| Software | Approved catalogue; package requests go through a review route | Approved, pinned versions; no self-service installs | Same as Locked (L2) |
| Internet | Only destinations the project policy names; some paths not covered | None; only approved internal services | Same as Locked (L2) |
| Data | Approved datasets and project working areas | Approved, versioned datasets, mounted read-only | Same as Locked (L2) |
| AI | Catalogue models; external endpoints only with approval from the project and the data owner; governed agents | Approved AI and machine-learning code inside batch jobs; no outside model or API calls; no agents | Same as Locked (L2) |
| Outputs | Airlock; at least one qualified independent checker | Airlock; two independent checkers, both approve | Same as Locked (L2) |

&nbsp;

Controlled feels like ordinary Nuvolos inside a governed perimeter. Locked feels like sending your code to the data and reading the results later. Enhanced runs on a dedicated deployment with tighter operator access. The operator runs the underlying infrastructure. The operator may be Nuvolos, your organisation or a provider. It is not a project role.

## Your working environment

Your working environment has several storage areas, and each one behaves differently. Check which area holds your work before you end a session.

### Storage areas

| Area | Shared with | Survives restart | In snapshots | Use for |
| :---- | :---- | :---- | :---- | :---- |
| Workspace | Everyone using the instance | Yes | Yes | Shared project files and team working data |
| Personal | Yours alone in that instance by default. In shared-mode applications, the home area is shared by all users. | Yes | Yes | Your own notebooks, scripts and drafts |
| Application | Everyone using that application in the instance | Yes | Yes, with the application configuration and installed packages | Installed packages and application settings |
| Temporary (ephemeral) | Only the running session | No. Erased when the session stops. Keep anything you need in a persistent area. | No | Scratch files during a computation |
| Large File Storage, where the deployment uses it | Applications that mount it | Set per deployment | No | Very large, mostly static data. Retention is set per deployment. |

&nbsp;

Personal areas can be captured in snapshots, and space administrators can reach them. They are not a confidentiality boundary.

Workspace, Personal and Application areas persist across application restarts. Temporary storage does not, so save outputs to a persistent area during long computations.

Copying data inside the project follows the access rules of the instance and the dataset. Those rules are your instance role and the dataset's approval. Moving content into another project is a governed crossing. It is not a copy.

In Locked (L2) and Enhanced (L3), you work in isolated run storage, and results go to the run's output area. See the batch job walkthrough below.

### Effective access

Nuvolos shows who can reach your project, each dataset and each instance, and why. Each access has a basis: an explicit grant, a role derived from another role, an automatic assignment or a dataset approval. An access whose origin cannot be determined appears as unknown.

Joining a project does not make you an editor. An editor role comes from an explicit invitation or an administrative assignment. An invitation does not approve a dataset.

Before you work, complete your organisation's onboarding and access requirements. Sensitive work also waits until the project and dataset approvals are in place.

Instance roles decide what the platform lets you do. An instance role is the role you hold on a specific instance.

| Activity | Editor | Viewer | Observer |
| :---- | :---- | :---- | :---- |
| Read files | Yes | Yes | No |
| List files | Yes | Yes | Yes |
| Download files | Yes (L0 only) | Yes (L0 only) | No |
| Query tables | Yes | Yes | No |
| Modify files | Yes (L0,L1), limited (L2,L3) | No | No |
| Create snapshots | Yes | No | No |
| Start applications | Yes (L0, L1 approved catalogue), No (L2,L3 batch only) | No | No |
| Invite users, create instances, change space configuration | No | No | No |

&nbsp;

A space administrator is treated as an editor on every instance in the space, in Open (L0). TRE levels (L1,L2,L3) separate administration from data access. Grant that role only to people who are authorised to read everything in the project.

## Sessions behind the remote-desktop sidecar

In Controlled (L1), no application interface reaches your browser directly. A remote-desktop sidecar sits between each application and you. It controls what can move in and out of the session.

1. You start an application. It runs in its own container inside the project.  
2. The application listens only inside the workload. Only the sidecar can reach it.  
3. The sidecar shows the application in an isolated browser for web apps, or in a desktop session for desktop apps.  
4. You see the screen. The sidecar streams only the screen to you. Clipboard and file movement pass through separate controls.  
5. Every clipboard or transfer attempt is logged with its direction, size and outcome. The log never records the content.

The table shows what you can and cannot move.

| Action | Result | What to do instead |
| :---- | :---- | :---- |
| Copy text out of the session to your device | Capped and logged on browser desktops, not blocked. Other channels are uncovered. The setting cannot be changed. | Send results through an output request. Do not retype or photograph them. |
| Paste text into the session from your device | Allowed up to a size limit. Each paste is logged. Project policy can block, limit or allow it. | Paste small snippets. Bring larger material through an import request. |
| Transfer files into or out of the session | Blocked in both directions | Use an import request for inbound files and an output request for outbound files. |
| Download from the in-session browser | Disabled | Use an output request. |
| Print from the in-session browser | Disabled | Use an output request. |
| Open the application's direct address | Not exposed | Work through the session window. |

### Limits

- The sidecar controls clipboard and transfer, not pixels. Screenshots, photographs, retyping and on-device text recognition remain possible at every level.  
- Streaming adds latency to interactive work.  
- Paste-in brings data into the session, so it is a data-entry route as well as a convenience.  
- An application that cannot run behind the sidecar is not offered at Controlled (L1). An exception is possible only if it is recorded on the verdict page.  
- Nuvolos lists browser surfaces and web IDEs without a server-side control point as uncovered. It does not count them as protected.

## Software and packages

Your project can use only the software in its catalogue, at approved versions.

### The catalogue

Nuvolos builds your project's catalogue from three sources. These are what the deployment supports, what the project's protection level and agreement permit, and any licences the organisation has arranged. Entries can include familiar tools such as JupyterLab, RStudio and VS Code. Some applications use a bring-your-own-licence arrangement. Check the licence before you plan work around one.

If something is not in the catalogue, raise a software request. The request names the tool, the version, the purpose and any licence details.

1. Submit a software request through the route your deployment documents, usually support or the project administrator.  
2. A named human decision-maker, such as the project owner or manager, the space administrator or the operator, as agreed for your deployment, accepts or refuses it. You cannot approve your own request. An agent never approves.  
3. If it is approved, the software appears in the project catalogue as a supported configuration.

Refusals usually give one of four reasons: no licence, incompatible with the protection level, no approved version, or a security review outcome that the deployment cannot support.

### Versions and pinning

In Locked (L2) and Enhanced (L3), only approved, pinned versions run, and self-service installs are off. In Controlled (L1), each catalogue entry carries approved versions. Ask for a different version through a software request.

### Packages

Whether you can add packages depends on the project's review route.

- If the project has the package review route, request packages through it.  
- If it does not, use what the approved environment provides. Raise a software request for anything else.  
- Packages installed into an application stay in that application's Application area. They travel with its snapshots.  
- A failed install shows the installer error. The usual causes are a package source that is not allowed, or self-service being off for the project.

Example: A researcher needs a statistical package that the environment does not provide. They raise a software request that names the package, its version, its purpose and its licence. Until it is approved, they use an alternative that is in the catalogue.

### Containers and images

Export of an application as a Docker image is not available in a TRE project. Custom containers and self-built images are outside the Controlled (L1) commitment unless your deployment's profile statement (the deployment's statement of which controls are enforced) says its image controls cover them.

### Recovering a broken environment

If an application stops working after a package change, use the smallest reset that fixes it.

1. Clear settings resets the configuration in your Personal area.  
2. Factory reset resets the application library, which holds your package installs.  
3. Restore the application from a snapshot if the first two steps do not fix it.

### Limits

- Nuvolos records the image each session ran from. The record shows what ran. It does not prove that the image was approved.  
- Where approved-image checks are not enforced, an unapproved image can run.

## Budgets and compute

Wallets and accounts hold spending limits. They have a credit balance. A displayed balance or allowance is automatically a hard cap.

The balance is used to fund the following resources:

* Interactive compute runs (L0,L1)  
* Batch job runs (L0,L1, L2, L3)  
* Agentic workflows (L0, L1 with exceptions)  
* Storage (L0,L1,L2,L3)

Credit balance is a hard cap: once balance is depleted (balance \< 0), all interactive and batch compute jobs are terminated. Nuvolos does not allow starting jobs and runs that will deterministically terminate due to balance depletion during their course.

To protect your work from a budget stop:

1. Check usage against the budget before you start a long computation.  
2. Save intermediate results to a persistent area as the work runs.  
3. Stop sessions you no longer need. Stopping ends the session compute charge. Nuvolos implements automatic stopper safeguards, but these may take 12-24 hours to trigger depending on space settings.  
4. For batch jobs, write checkpoints to the output area while the job runs, where your code allows it.

### Limits

- Storage and other separately metered services can still incur charges after a session stops.  
- Cost controls are not access controls. Enabling elastic sizes or GPUs never widens who can see which data.

## Working in Controlled (L1)

In Controlled (L1), you start permitted applications, open approved data and save your work in the project. Your work lives in the storage areas described above, so check them before you stop.

Starting an application creates a session with its own identifier. A session can be refused at start if its image is not permitted, its elastic size is not enabled, or the project does not allow interactive work.

Session history records start, stop, runtime and size for each session. A session stops when you stop it, after a period of inactivity, when an operator acts, or when the deployment's budget configuration stops it because its budget is used up. Check the session history for the reason.

Session logs hold the session's own output. They can contain sensitive content, and they are separate from the audit trail. Session logs are kept for only a few days today. Save anything you need to keep in a persistent area. Only the person who started a session can see its logs. For shared-mode applications, project members can see them. In shared mode, everyone using the instance shares one running application and one home area. Do not put personal credentials in a shared home.

You must not:

- Use download links, application export, snapshot download, or publish and distribute features. Where the deployment evidences it, the platform refuses them under the project's policy and opens a request form instead.  
- Export an application as a Docker image. That feature is not available in a TRE project.  
- Use git clones, external cloud mounts or external storage to move data out, unless your project policy names them.  
- Send project data to a model or service outside the project unless the project and data owner have approved that destination.  
- Put personal credentials in a shared home area.  
- Move content into another project. That is a governed crossing, not a copy.

## Working in Locked (L2) and Enhanced (L3)

In Locked (L2) and Enhanced (L3), you do not open an interactive session on the sensitive data. You submit analysis code that runs as a batch job against an approved, versioned dataset. The only interactive exception is a contained reviewer session, which checkers use to inspect staged results.

### Batch job walkthrough

1. **Prepare the code.** Write code that reads the approved dataset version as read-only input. Write results to the run's output area. Clear notebook outputs, and remove sample records, keys and tokens.  
2. **Declare the environment.** List each approved software package and the approved, pinned version the job needs. Name the dataset version. Ask only for resources within the approved set.  
3. **Submit.** The platform checks the job against the project's approved software and resources before it starts. A refused job shows the reason in its run record. Request what is missing, then submit again.  
4. **Run.** The job runs in isolated storage. It has no internet access and reaches only the approved internal services it needs. Approved AI and machine-learning software can run inside the job. Outside model or API calls cannot.  
5. **Follow progress.** The run record shows the job's status and what the job used.  
6. **Collect outputs.** Outputs go to the run's output area. Nothing becomes a file for release automatically, so stage only what you need.

Example: A job needs a specific approved version of a statistics library. The declaration names that version. If the job asks for a version that is not approved, the platform refuses it, and the run record shows the reason. The researcher raises a software request and resubmits once the version is approved.

### Run record fields

| Field | What it shows |
| :---- | :---- |
| Run status | The job's current state, from submission to completion or failure |
| Refusal reason | Why the platform refused the job before it started, and the next step |
| Declared environment | The approved software and versions the job declared |
| Dataset version | The approved, read-only version the job read |
| Resources used | What the run consumed against its approved resources |
| Recorded image | The image the job ran from. It shows what ran, not that the image was approved. |

### Output area and staging

The run's output area stays inside the project. Nothing leaves it until you stage files and submit an output request. The output area is not the staging area. It holds a run's raw results. The staging area holds the exact bytes you submit for release.

1. Check each output before you stage it.  
2. Copy the exact files you want to release into the project's staging area.  
3. Build the output request, as described in the next section.

Changing a file after you submit an output request invalidates the frozen manifest. Finish all edits before you submit.

### Limits

- Batch jobs run only on approved, pinned software. A job that needs a new package waits for a software request.  
- A job cannot reach the internet or call an outside model. Locked (L2) has no runtime agents.

## Getting results out

Results leave only through the output airlock, and a human decides every release. The airlock checks the exact bytes you submit, not the files you meant to send. The steps below take a result from staging to delivery.

1. Choose the exact files and state their intended use. If you try a refused route, such as a download link, the platform opens a request prefilled with those items.  
2. Stage the exact bytes in the project's staging area. You can not copy them to a laptop, a share link or a chat attachment.  
3. Submit the request with a frozen manifest. The manifest lists every item with a checksum of its bytes, and it is written once. Anything staged but missing from the manifest is held for human review.  
4. Automated disclosure checks run where the project configures them. Their report advises the checker. A missing report shows "check not performed", and it never counts as a pass.  
5. Checkers review the frozen manifest. In Controlled (L1), at least one qualified independent checker reviews it. In Locked (L2) and Enhanced (L3), two independent checkers review it in a contained reviewer session that cannot download the material, and both must approve.  
6. The checker makes one decision, with reasons where needed:  
   - **Approve:** the checker approves the exact frozen content. The data owner or a delegate must still authorise release.  
   - **Return for changes:** nothing is released. You prepare a new version that addresses the reasons.  
   - **Reject:** the request closes with reasons, and the record is kept. You can submit a corrected request later.  
7. An approved result is delivered through a single-use link. The link expires and is bound to the named recipient's identity. It goes only to a recipient authorised under the data owner's policy. You receive it only if you are separately authorised. A failed transfer shows as not delivered. Reissuing access is a new governed action.  
8. If any byte changes after approval, the approval no longer applies. The changed content is re-manifested and reviewed again.

### Who decides

| Role | Authority | Cannot be |
| :---- | :---- | :---- |
| Requester (you) | Creates and submits the request. Responds to requested changes. | The checker on your own request |
| Data owner or delegate | Holds release authority under the data agreement. Can nominate a delegate. | Anyone not authorised under the data agreement |
| Checker | Examines the frozen request and records a decision | The requester, the sponsor of any agent involved, or any agent, service or machine identity |
| Recipient | Receives approved content through a single-use link | Anyone not authorised under the data owner's policy |
| Project administrator | Assigns checkers and runs the review queue | A substitute for the data owner's authority |

You cannot be the data owner or delegate who releases your own request. At Locked or Enhanced, neither checker can release.

The data custodian runs dataset intake and approves each dataset version. The data owner holds release authority for outputs. These may be different people. The project administrator here assigns checkers and runs the review queue. That duty is administrative. It is not release authority.

Your request moves through five states:

| State | Meaning |
| :---- | :---- |
| Submitted | The frozen manifest is accepted, and checks are pending or complete. |
| In review | A checker is examining the request. |
| Decided | Approve, return for changes, or reject is recorded. |
| Delivered | The authorised recipient has retrieved the approved content. |
| Withdrawn or expired | The request is closed. It was never released. |

Waits are measured and shown, not promised. Nuvolos does not promise a decision time. Overdue requests escalate or expire, and they never release automatically. If no checker is available, the output stays inside the project.

### What checkers look for

Checkers look at each item. They also look at how it relates to earlier releases from the same project. The table lists the usual concerns and what helps.

| Output | What the checker looks for | What helps |
| :---- | :---- | :---- |
| Tables and result sets | Small counts that could identify a person, and values that can be derived | Aggregate results, and apply the project's small-cell threshold |
| Repeated releases | Differencing: safe-looking releases that together reveal a suppressed value | Explain how each release relates to earlier ones, and avoid near-duplicate cuts |
| Code and notebooks | Embedded data, sample records in cell outputs, and credentials | Clear cell outputs, and remove data, keys and tokens before staging |
| Models and weights | Memorised records. A model is not safe merely because it is not the dataset. | Agree the export policy before training. Models stay inside by default. |
| Figures and documents | Small extracts and identifiable detail | Keep extracts minimal, and check captions and annotations |
| Logs, prompts and AI records | Project data that may contain sensitive content | Stage only what you need, and review them like any other output |
| Packages and archives | Contents, not filenames | List every file in the manifest, and do not bundle extras |

Binary and proprietary files may not be inspectable. Project policy decides whether they can leave. The checker records the basis for the decision.

### Writing an output request well

A clear request helps the checker decide without a return for more information. Write the purpose and usage note for a checker who has not seen your analysis. Each item in the manifest needs these fields.

| Field | What to enter |
| :---- | :---- |
| Item | Each file or item in the staging area |
| Checksum | Recorded for each item from its exact bytes, at submission. Written once. |
| Output kind | Table, figure, code, document, model, log, package or archive |
| Source | The approved dataset version and the analysis code that produced the item |
| Purpose and usage note | What the output is, why you need it, and who will use it |
| Disclosure steps | The thresholds you applied, the rows or columns you removed, and the values you aggregated |
| Relation to earlier releases | How the item relates to earlier releases from this project |
| Recipient | Set under the data owner's policy. You do not choose it. |

A good purpose and usage note states five things:

- What the output is, in one sentence.  
- Which dataset version and code produced it.  
- Who will use it, and for what purpose.  
- Which disclosure steps you applied, and what you removed.  
- How it relates to earlier releases, including any near-duplicate.

Example: "Table of counts by region for the funding report. Produced from the approved dataset version and analysis code at the version listed. Cells under the project threshold are merged into an other group. It differs from the previous quarter's release only in one age band."

### Preparing each output type

- **Tables:** Aggregate to the level the question needs. Apply the project's small-cell threshold. Remove any value that can be worked out from another row or from a total.  
- **Code:** Clear all cell outputs. Remove data, keys, tokens and passwords. Check comments for sample records.  
- **Figures:** Keep extracts minimal. Plot summary values rather than individual records where you can. Check captions, axis labels and annotations.  
- **Models:** Agree the export policy before training. A model stays inside by default. Do not stage weights or fitted model objects unless the agreed policy allows it.  
- **Logs and AI records:** Stage only what you need. Review them like any other output.  
- **Packages and archives:** List every file in the manifest. Do not bundle extra files.

### Disclosure-control checklist

Work through this list before you submit the request.

- [ ] Every item in the staging area is in the manifest, and every manifest item is in the staging area.  
- [ ] Each table applies the project's small-cell threshold, and no value can be worked out from another row or total.  
- [ ] Code has no cell outputs with records, and no keys, tokens or passwords.  
- [ ] Figures show no individual record. Captions and annotations are checked.  
- [ ] No model weights or fitted model objects are staged unless the agreed export policy allows them.  
- [ ] Logs and AI records are staged only where needed.  
- [ ] Archives contain only the files listed in the manifest.  
- [ ] The purpose and usage note states the source, the disclosure steps and the relation to earlier releases.  
- [ ] All edits are finished. Any later change needs a new manifest and a new review.

### Limits

- The automated check report assists the checker. It never decides, and a missing report is never a pass.  
- Binary and proprietary files may not be inspectable, so the project policy decides whether they can leave.

## Worked examples

These examples use generic values. Your project's thresholds, approvals and software will differ.

### Example 1: Controlled (L1), importing a dataset and releasing two summary tables

1. You submit an import request. It names the project, the source, the dataset, its intended use, any licence, and the dataset name and version it is published under.  
2. The material stays in quarantine while the checks run. Each check result is recorded. A check that is not configured shows the status not scanned.  
3. The data custodian reviews the request and approves it. You cannot approve your own request. The dataset appears in your project as a read-only, versioned input.  
4. You open an interactive application in your instance and mount the dataset read-only. You do your analysis and save derived files in Workspace or Personal.  
5. You produce two tables. One gives counts by region. The other gives mean values by age band. Apply the project's small-cell threshold. Check that no value can be worked out from another value.  
6. You stage the two tables in the staging area. You write the purpose and usage note, and you submit the request with its manifest.  
7. The advisory check report is attached to the request. One qualified independent checker reviews the frozen manifest and approves it.  
8. The data owner or an authorised delegate then authorises release. The approved tables go to the authorised recipient through a single-use link.

### Example 2: Locked (L2), a batch regression job and releasing coefficients

1. You prepare the code. It reads the approved dataset version as read-only input. It fits a regression and writes three items to the output area: a coefficient table, a fit summary, and a plot of fitted values against observed group means. The plot shows group summaries, not individual rows. You clear the notebook outputs.  
2. You declare the environment. It lists the approved, pinned statistics software and the dataset version. Its resources sit within the approved set.  
3. You submit the job. The platform checks it against the approved software and resources, and the run record shows the job as accepted.  
4. The job runs in isolated storage with no internet access. The run record shows its status and what it used.  
5. You decide what to release. The coefficient table and the fit summary are the results. The fitted model object stays inside, because a model can memorise records. The export policy for models was agreed before training.  
6. You stage the coefficient table and the fit summary. The purpose and usage note says the coefficients come from the approved dataset version, and that the confidence intervals are rounded and small groups are merged.  
7. Two independent checkers review the request in contained reviewer sessions. Both must approve. The data owner or an authorised delegate then authorises release.  
8. The approved items go to the authorised recipient through a single-use link.

If you later change the rounding, the approval no longer covers the changed bytes. The changed item needs a new manifest and a new review.

### Example 3: Returned for changes, then resubmitted

1. A checker returns a figure for changes. A point label shows the exact value for a small group, and the decision gives that reason.  
2. You read the reason. You remove the label and merge the small group into an other category.  
3. You revise the figure in the session and replace the old item in the staging area with the revised file.  
4. You build a new manifest with new checksums. The purpose and usage note explains the change, and it states how this figure relates to the earlier release. The checker compares the request against earlier releases.  
5. You submit the new version. The earlier decision does not cover the changed bytes, so the item is reviewed again.  
6. The checker approves the item, or rejects it with reasons. A rejection closes that submission. You can submit a corrected request later.

## When something is blocked

Find the symptom in the table and take the next step. Most refusals give a reason. The reason tells you which request to raise.

| You see | Why | What to do |
| :---- | :---- | :---- |
| Access denied | You lack the required instance role or the dataset approval | Ask the project manager to check your role. Ask the data custodian to confirm the dataset approval. An invitation does not approve a dataset. |
| Import held | A required check is pending, failed or unavailable, or it was not configured | Check the status and reason. Correct the material, or wait for review. A failed or unavailable required check never turns into an approval. |
| Application will not start | It is not in the catalogue, its licence is missing, or its elastic size is not enabled | Raise a software or entitlement request. |
| Tool you used in open Nuvolos | Not automatically allowed in a TRE project | Request it through the approved software or connection process. |
| Image refused at launch | The image is not on the approved list | Request the software through the catalogue route. |
| Package install fails | The package source is not allowed, or self-service is off | Use an approved source, or request the package. |
| Connection or mount refused | The connector is not on the project's list | Request the connector, or move the data through the import airlock. |
| Paste refused or limited | Paste-in is capped in size, or project policy blocks it | Paste a smaller snippet, or bring the material through an import request. Ask the project manager about the policy. |
| Copy or transfer out refused | Copy-out and file transfer out of the session are blocked | Use an output request. Do not retype or photograph results. |
| Download, print or direct address unavailable | Downloads and printing from the in-session browser are off. The application's address is not exposed. | Use an output request for anything that must leave the project. |
| Download or export refused | Direct export routes are closed in a TRE project | Use the request form that the refusal opens. |
| Batch job refused | Software, versions or resources are not approved for the project | Read the reason in the run record. Request what is missing. |
| Batch job stopped | The deployment's budget configuration stopped it, or an operator acted | Check the run record for the reason. Restore checkpoints from the output area or a persistent area. |
| Session stopped | Inactivity, an operator action, or a deployment budget stop | Check session history for the reason. Restore saved work from persistent areas. |
| New work refused | A budget is used up, or the resource configuration does not permit the work to start | Check usage against the budget. Ask the project manager to review it. |
| File missing | You are in the wrong instance, or the file was in temporary storage | Check each persistent area. Temporary content cannot be recovered. |
| Output returned for changes | The checker found an issue | Revise the content and resubmit. An old approval cannot cover changed content. |
| Output stays inside | No qualified checker is available | Check the request status. Ask the project manager to escalate. |
| Delivery link expired or failed | Links are single-use and time-limited | Ask for reissue through the governed flow. Do not reuse the link. |
| Agent refused or paused | A pause is active, or the action is outside the agent's authority | Check with the agent's sponsor. Use Stop for running agent work. |
| Logs unavailable | They are outside the deployment's retention window | Check the profile statement. Save important logs inside the project as data. |
| Suspected incident | Something looks wrong with data, access or an output | Stop the activity if you can. Contact the project and TRE incident contacts. Do not use ordinary support. |

## Limits

Nuvolos does not remove every disclosure path. The limits below apply across the project, in addition to the limits in each section.

- SATRE is a self-assessment of an operated deployment. It is not a certification of Nuvolos.  
- Controlled (L1) does not contain the reviewer. There is no contained reviewer session at L1. A checker works inside the project with an ordinary platform identity.  
- Deleting a file removes it from view. Nuvolos reports residual copies per data plane, with a stated end date for each. It never reports a deletion as complete while a copy remains.  
- Audit trails are tamper-evident, not tamper-proof. Decision receipts are recorded but unsigned. Records start when capture starts. They cannot backfill earlier events.  
- Operators are never blind to project content. Operator access needs break-glass, meaning emergency operator access. Break-glass requires a ticket, a second approver, a defined scope, an expiry, notice to your tenant's designated incident or security contact, and a record.  
- Enhanced (L3) is not operator-blind, not air-gapped, and does not use confidential computing. Its controls are set out in the deployment's profile statement.  
- Retention, residency and key custody are set for each deployment. No single setting applies everywhere.  
- Deleting a secret inside Nuvolos does not revoke it at the external service. Rotate or revoke the credential there.  
- Nuvolos does not promise review times. Any timing commitment sits in your organisation's service agreement.