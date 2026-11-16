# Part 10 — Reporting, capstone, and retesting

Lessons 64–70 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 64 | L-038 | 7 | Common attack techniques and detection |
| 65 | L-039 | 7 | Professional security reporting |
| 66 | L-048 | 7 | Capstone: Review a small lab system |
| 67 | L-049 | 7 | Track security findings to closure |
| 68 | L-068 | 7 | Writing clear evidence for security findings |
| 69 | L-069 | 7 | Writing a remediation plan |
| 70 | L-070 | 7 | Capstone retest and closure |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-038 — Common attack techniques and detection

### Simple explanation and real-world example

Defenders recognize patterns such as many failed sign-ins, unusual access, and unexpected file changes. Patterns help decide where to look next.

### Technical explanation

An indicator is a signal to investigate, while a technique is a general way an attacker pursues an objective. Credential guessing and misuse of a valid account may leave different evidence. Audit trails record actions for later review.

### Demonstration

Read two fictional records: one shows repeated sign-in failures across several accounts, and one shows a regular account editing a restricted setting after a normal sign-in.

### Hands-on exercise

Match each record to a possible pattern, then list one additional record or control that could confirm, explain, or prevent it.

### Expected result

Repeated failures may indicate a guessing attempt. A restricted change may indicate missing authorization, misuse, or an incorrect role assignment. Your notes should distinguish these possibilities.

### Knowledge check

1. What is an indicator?
2. How can many failures inform triage?
3. Which access record could clarify why a regular account edited a setting?

### Mini challenge

Consider an authorized maintenance window that overlaps the activity and explain what you would recheck.

## L-039 — Professional security reporting

### Simple explanation and real-world example

A security report turns technical observations into work that a team can prioritize and verify later.

### Technical explanation

A finding is a documented security issue. Evidence establishes the observed condition. Impact explains what could happen. Remediation describes the repair. Verification states how to tell whether it worked.

### Demonstration

Read a concise example: “Viewer role can edit training records. The lab permission matrix grants viewers Write where the approved policy requires Read. Remove Write from viewers and verify that they can still open records.”

### Hands-on exercise

Write a single finding for a fictional practice folder. Give it a title, condition, evidence, impact, fix, and verification step.

### Expected result

A reader should be able to trace the impact to the condition and reproduce the verification using the approved evidence or test results. Separate actual observations from possible consequences.

### Knowledge check

1. What belongs in the evidence section?
2. How does impact differ from the condition?
3. What does a useful verification step describe?

### Mini challenge

Write a two-sentence summary of the finding for a manager who does not need configuration details.

### References

- [NIST Security Testing Guide · reporting sections](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf)

## L-048 — Capstone: Review a small lab system

### Simple explanation and real-world example

A capstone combines the earlier skills in one realistic review. Small, well-documented findings are enough for a complete exercise.

### Technical explanation

An executive summary explains the most important result in plain language. An evidence register lists supporting records. A retest criterion specifies how success will be judged.

### Demonstration

Use this fictional brief: File-Lab expects Alice to edit and Sam to read. The settings export shows both can write. The event log shows Sam opened a file at 10:15. An updated settings export shows Sam now has read access only.

### Hands-on exercise

Write a short report with scope, one confirmed finding, an evidence table, a recommended fix, and a verification plan. Mention what the log shows and where its conclusions stop.

### Expected result

The original settings confirm excessive write access. The log shows an open event. The updated settings support the fix, and a functional check would confirm the expected read and write behavior.

### Knowledge check

1. What proves the original weakness?
2. Does the open event establish a write occurred?
3. What evidence would verify that the fix works?

### Mini challenge

Add a one-paragraph executive summary for a nontechnical lab owner.

## L-049 — Track security findings to closure

### Simple explanation and real-world example

A finding moves from discovery to closure when someone owns it, applies a fix, and verifies the result.

### Technical explanation

The remediation owner coordinates the repair. Acceptance criteria define the evidence required for closure. A finding can remain open while a fix or retest is pending.

### Demonstration

Start with the File-Lab finding. Assign a fictional owner, note that a permissions change is ready, and require a documented check showing a viewer can read and cannot edit.

### Hands-on exercise

Make a one-row record with finding ID, owner, status, acceptance criteria, and evidence. Leave the finding open while evidence is missing.

### Expected result

The row should make the next action obvious. An updated setting supports the change. Functional evidence supports closure against the criteria.

### Knowledge check

1. Who owns the repair?
2. Why write closure criteria up front?
3. What should happen when verification is pending?

### Mini challenge

Add a second record that is blocked by missing access to approved evidence and state what information would unblock it.

## L-068 — Writing clear evidence for security findings

### Simple explanation and real-world example

Someone reading your finding should be able to see exactly what supports it. Clear evidence is specific, limited to relevant details, and safe to share.

### Technical explanation

Evidence provenance records where it came from and when it was collected. Sanitization removes unnecessary sensitive details. Observation describes what a record directly shows.

### Demonstration

Use a fictional settings line: Group=Viewers; Access=Read,Write; Policy=Read. Name the source as Approved lab configuration export and add a sample timestamp.

### Hands-on exercise

Write a finding paragraph and quote only the fields needed to support it. Include the source, a timestamp, and a sentence about what the record confirms.

### Expected result

Your paragraph identifies the mismatch without claiming that anyone actually wrote a record or revealing unrelated identifiers.

### Knowledge check

1. What does provenance record?
2. When should evidence be sanitized?
3. Which claim does this configuration directly support?

### Mini challenge

Rewrite an overly broad claim such as all users abused write access so that it matches the supplied evidence.

## L-069 — Writing a remediation plan

### Simple explanation and real-world example

A remediation plan turns findings into tasks that a team can carry out, assign, and verify.

### Technical explanation

An owner is accountable for a task. A corrective action addresses the condition. Verification criteria define observable success. A dependency is something that needs to happen first.

### Demonstration

Consider three fictional findings: unnecessary write access, missing alert ownership, and stale software. Assign the folder owner, monitoring team, and service team to the respective fixes.

### Hands-on exercise

For each case, write the owner, ordered action, evidence needed for completion, and one dependency if relevant.

### Expected result

The three rows should specify concrete changes. For example, the access fix should include a successful read and a blocked viewer edit.

### Knowledge check

1. What makes an action verifiable?
2. Who should own an alert routing change?
3. When does a dependency belong in the plan?

### Mini challenge

Order the three changes for a fictional release window and explain which one comes first.

## L-070 — Capstone retest and closure

### Simple explanation and real-world example

Retesting compares new evidence against the same rule used in the original finding. It provides the basis for closure.

### Technical explanation

Fixed means the stated criterion is met. Partially fixed means part of it is met. Open means the issue remains or its closure criteria are still unverified. Record the date and evidence with the outcome.

### Demonstration

Review these fictional retests: A now blocks viewer writes and still allows reads. B blocks local edits but approved evidence shows the same role still has write access through a second interface. C has no new evidence.

### Hands-on exercise

Classify A, B, and C. Write a sentence for each that explains the observed result and identifies remaining work if applicable.

### Expected result

A is Fixed, B is Partially fixed, and C remains Open pending evidence. Each label should follow the written criteria.

### Knowledge check

1. Why retest against the original criteria?
2. What makes B only partially fixed?
3. Which evidence should be preserved for a closed finding?

### Mini challenge

Draft a one-line closure record for A with a status, date placeholder, and evidence reference.
