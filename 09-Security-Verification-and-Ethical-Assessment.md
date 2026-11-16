# Part 09 — Security verification and ethical assessment

Lessons 57–63 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 57 | L-047 | 6 | Verify a security fix |
| 58 | L-065 | 6 | Browser cookies and session settings |
| 59 | L-066 | 6 | Alert triage and false positives |
| 60 | L-067 | 6 | Compare two network captures |
| 61 | L-035 | 7 | Assessment scope and testing methodology |
| 62 | L-036 | 7 | Reconnaissance and enumeration |
| 63 | L-037 | 7 | Vulnerability assessment and prioritization |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-047 — Verify a security fix

### Simple explanation and real-world example

A change is complete when you can show that the old problem is gone and the permitted workflow still works.

### Technical explanation

A verification criterion states what should happen if a fix works. A regression is a new break caused by a change. Evidence records the actual observed result.

### Demonstration

Use a practice access matrix where readers initially edit a file. The corrected matrix allows them to read while restricting edits to the owner.

### Hands-on exercise

Write three test results using the fictional data: reader opens file, reader saves changes, owner saves changes. Mark expected, observed, and outcome for each.

### Expected result

A good result records allowed, blocked, allowed in that order. A blocked legitimate owner action would reveal a regression.

### Knowledge check

1. What belongs in a verification criterion?
2. Why test the owner as well?
3. What makes a retest useful to someone else?

### Mini challenge

Add an outside account and write the expected result and the evidence you would keep.

## L-065 — Browser cookies and session settings

### Simple explanation and real-world example

A website can remember a session by saving a cookie in the browser. Cookie settings limit the circumstances under which the browser exposes or sends it.

### Technical explanation

Secure limits sending to secure connections, HttpOnly limits access by browser scripts, and SameSite controls sending cookies in certain cross-site requests. A session cookie can carry an identifier the server uses to look up a session.

### Demonstration

Inspect this sample header on paper: Set-Cookie: session=demo; Secure; HttpOnly; SameSite=Lax. Circle each setting and connect it to its purpose.

### Hands-on exercise

Compare the sample with a second fictional header that contains only Secure. Write what browser restrictions are absent from that header.

### Expected result

The first header declares all three restrictions. The second omits explicit HttpOnly and SameSite settings. Browser defaults may still affect cross-site behavior.

### Knowledge check

1. What does Secure control?
2. What does HttpOnly restrict?
3. Why specify SameSite deliberately?

### Mini challenge

Write a fictional review comment explaining which settings a team should verify for its session cookie.

## L-066 — Alert triage and false positives

### Simple explanation and real-world example

A security alert is a signal to investigate. Some alerts turn out to be ordinary activity, while others need urgent attention.

### Technical explanation

An indicator is an observation that may point to an issue. A false positive is an alert that incorrectly labels benign activity as a concern. Triage looks at evidence, impact, and urgency.

### Demonstration

Review three fictional alerts: three failures from a known employee device followed by normal success; dozens of failures across many accounts from an unexpected source; an approved backup job running on schedule.

### Hands-on exercise

Choose which alert you would review first. Cite two details from the sample and name one record that would strengthen the conclusion.

### Expected result

The numerous cross-account failures give the strongest reason to investigate promptly. The other examples may be benign after verifying the surrounding context.

### Knowledge check

1. What makes an alert different from a confirmed incident?
2. What evidence makes the second example more urgent?
3. What does false positive mean?

### Mini challenge

Write a short alert disposition with an outcome and the evidence that supports it.

## L-067 — Compare two network captures

### Simple explanation and real-world example

Comparing a working request with a failing one helps isolate the reason. A DNS answer can report success, a missing name, or other outcomes.

### Technical explanation

A DNS response code describes the result of the lookup. NOERROR indicates no DNS protocol error. NXDOMAIN indicates the requested name does not exist according to the response.

### Demonstration

Use two supplied exercise captures if available. Otherwise use this sample summary: A queried shop.example and returned NOERROR with address 192.0.2.10. B queried shpo.example and returned NXDOMAIN.

### Hands-on exercise

Compare the two queries and responses. Record the name, result, answer data if present, and your diagnosis.

### Expected result

A provides an answer. B shows a failed name lookup and the query contains a spelling difference from the working example. NOERROR alone does not guarantee an address record is present.

### Knowledge check

1. What does NXDOMAIN report?
2. Which field reveals the spelling difference?
3. What else should you check after seeing NOERROR?

### Mini challenge

Write a third fictional result for a query that has no response in the available capture. Explain why that differs from NXDOMAIN.

## L-035 — Assessment scope and testing methodology

### Simple explanation and real-world example

A security assessment starts by deciding which systems, evidence, and actions are in scope. The report needs to explain how conclusions were reached.

### Technical explanation

Scope defines the allowed systems, boundaries, time window, and methods. Rules of engagement record approved activities, limits, and contacts. Verification checks whether a fix changed the observed condition.

### Demonstration

Read this fictional assignment: review the supplied settings and event records for two lab VMs, document access issues, then check sample results from after remediation.

### Hands-on exercise

Write a one-page scope with the objective, two lab systems, allowed evidence sources, expected report, and a contact for questions about scope.

### Expected result

Your scope should let someone tell whether a proposed action is permitted. The assessment method should produce evidence that can be reviewed later.

### Knowledge check

1. What does scope define?
2. Why name permitted methods?
3. At which point should you confirm the results of a fix?

### Mini challenge

A third VM appears in the inventory. Write how you would log that discovery and resolve its status before reviewing it.

### References

- [NIST Guide to Security Testing and Assessment](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf)

## L-036 — Reconnaissance and enumeration

### Simple explanation and real-world example

Before assessing a system, find out which assets and services are documented. An accurate inventory makes wrong assumptions visible.

### Technical explanation

Reconnaissance gathers initial information. Enumeration organizes known resources into a more detailed list. Use authorized records such as lab asset lists and configured services in this course.

### Demonstration

A lab brief lists two assets: web-lab owned by the training app team and db-lab owned by the data team. A service record also lists a backup service on db-lab.

### Hands-on exercise

Create a table with asset name, owner, expected service, and evidence source. Mark one feature as unverified when the records do not support it.

### Expected result

Your inventory includes both assets, ties each entry to a record, and distinguishes an expected or documented service from confirmed operation.

### Knowledge check

1. What is the purpose of an inventory?
2. What can an asset record confirm?
3. Why label an assumption?

### Mini challenge

Add a service entry without an owner and describe how you would resolve the gap through authorized documentation.

## L-037 — Vulnerability assessment and prioritization

### Simple explanation and real-world example

An assessment finding should describe a confirmed condition, its impact, and how confident you are in the evidence.

### Technical explanation

Severity describes the seriousness of a condition. Confidence describes how strongly evidence supports the finding. Exposure and business impact help decide priority.

### Demonstration

Compare a configuration showing editors and viewers both have write access with a log entry that merely shows a viewer signed in. Only one provides direct evidence of the permission setting.

### Hands-on exercise

Draft one confirmed finding and one item marked for follow-up. Rank them and explain the evidence available for each.

### Expected result

Confirm the overly broad permission from the settings. The login supports a follow-up question about activity and does not establish that anyone used write access.

### Knowledge check

1. How does confidence differ from severity?
2. What evidence establishes the permission weakness?
3. Why track unconfirmed items separately?

### Mini challenge

Add evidence that viewers can edit a high-impact file and explain how it changes priority.
