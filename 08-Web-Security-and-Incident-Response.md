# Part 08 — Web security and incident response

Lessons 50–56 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 50 | L-029 | 6 | Network inventory with Nmap |
| 51 | L-030 | 6 | Web application security fundamentals |
| 52 | L-031 | 6 | OWASP Top 10:2025 |
| 53 | L-032 | 6 | Burp Suite Community Edition |
| 54 | L-033 | 6 | Log analysis and incident response |
| 55 | L-034 | 6 | Vulnerability identification and remediation |
| 56 | L-046 | 6 | Build an incident timeline |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-029 — Network inventory with Nmap

### Simple explanation and real-world example

A network inventory tells you which expected services are reachable. A record of open ports helps compare the lab’s actual state with its intended state.

### Technical explanation

A listening service accepts connections on a transport port. Nmap can list open, closed, and filtered results. A filtered result means filtering prevented Nmap from determining whether the port was open in that test.

### Demonstration

Read this sample Nmap-style output from a fictional lab: 22/tcp open ssh; 443/tcp open https; 8080/tcp filtered http-proxy. The lab inventory expects only 443/tcp to be reachable.

### Hands-on exercise

Compare the report with the expected inventory. Write which reachable service needs review and which result needs more evidence.

### Expected result

Port 22 is a confirmed difference in this report. Port 8080 is inconclusive from this observation. The labels alone do not verify the exact application or its configuration.

### Knowledge check

1. What does open mean in the report?
2. Why is filtered inconclusive?
3. What makes a listed service unexpected?

### Mini challenge

Write a three-column inventory table for expected service, observed state, and follow-up evidence.

## L-030 — Web application security fundamentals

### Simple explanation and real-world example

A web application sends requests between a browser and a server. The server should make access decisions for any protected action.

### Technical explanation

A session associates requests with a signed-in user. The server handles sensitive operations and authorization checks. A trust boundary is where data moves between parts that have different levels of trust.

### Demonstration

Draw Browser → Web server → Data store for a fictional grade portal. Add a request for a score and mark the point where the server checks that the user may see that record.

### Hands-on exercise

Draw the sign-in and read flow on paper. Label where authentication, session lookup, and record authorization occur.

### Expected result

Your result should show a separate record-level permission check at the server and explain what the browser sends to identify the session.

### Knowledge check

1. What does the server handle?
2. What does the session associate?
3. Why check record access on the server?

### Mini challenge

Add a teacher role and explain how the same server can apply different decisions to the same resource.

### References

- [OWASP Juice Shop project overview](https://github.com/juice-shop/juice-shop/blob/master/README.md)

## L-031 — OWASP Top 10:2025

### Simple explanation and real-world example

The OWASP Top 10 is a reference for common categories of web application security risk. It helps you describe what went wrong and ask for a suitable fix.

### Technical explanation

Risk categories group recurring problems. In the 2025 list, Broken Access Control and Security Misconfiguration are separate categories. The best label follows the evidence and root cause.

### Demonstration

Classify these descriptions: server lets a signed-in student see records outside their class; production server exposes verbose debug details because a deployment option was left enabled.

### Hands-on exercise

Compare the descriptions with the OWASP reference. For each case, name a likely category and one control that could address the underlying issue.

### Expected result

The expected categories are Broken Access Control and Security Misconfiguration. Your proposed controls should address scoped access and deployment settings respectively.

### Knowledge check

1. What does OWASP Top 10 organize?
2. What is broken access control?
3. Why tie your category choice to observed facts?

### Mini challenge

Classify a fictional service failure where important security events were recorded without any alerting process.

### References

- [OWASP Top 10:2025 overview](https://github.com/OWASP/Top10/blob/master/2025/docs/en/index.md)

## L-032 — Burp Suite Community Edition

### Simple explanation and real-world example

Burp Suite can show a record of web messages passing between a browser and a practice app. It helps you read request and response details.

### Technical explanation

A proxy sits between a client and server. HTTP history lists observed requests and responses. Headers carry metadata, and body content carries the data exchanged.

### Demonstration

In a local practice app with ordinary, authorized traffic, open one page normally in the configured Burp browser, then read one entry in Proxy’s HTTP history. For a no-install option, use this example: GET /catalog → 200 OK, Content-Type: application/json.

### Hands-on exercise

Record one method, path, status, and content type. Use an ordinary practice request and read only the response it produced.

### Expected result

A normal successful example should show GET, the requested path, status 200, and a content type. Some pages make several requests, so select the relevant entry.

### Knowledge check

1. What is a proxy?
2. Where do you find the response status?
3. What does Content-Type describe?

### Mini challenge

Compare the metadata of two normal page requests in the same local lab and explain one difference.

### References

- [PortSwigger HTTP history reference](https://portswigger.net/burp/documentation/desktop/tools/proxy/http-history)

## L-033 — Log analysis and incident response

### Simple explanation and real-world example

Incident response is how a team investigates a suspected problem, reduces harm, and restores normal service. Logs help build a shared account of what happened.

### Technical explanation

Triage is the initial review of urgency and scope. Containment limits harm. Recovery returns the affected system to normal operation. A timeline puts events in order.

### Demonstration

Review these fictional events: 09:05 repeated login failures for account A; 09:07 successful login for A; 09:10 a change to recovery settings. Use one time zone throughout.

### Hands-on exercise

Write a short timeline, one possible explanation, one piece of evidence still needed, and one fictional containment proposal.

### Expected result

The timeline should show the order of all three events. Separately identify the hypothesis and the logs that would support or challenge it.

### Knowledge check

1. What is triage?
2. What does containment aim to do?
3. Why preserve the order and time zone?

### Mini challenge

Add a confirmation that the account owner changed settings and explain how it affects your assessment.

### References

- [NIST Incident Response Recommendations](https://csrc.nist.gov/pubs/sp/800/61/r3/final)

## L-034 — Vulnerability identification and remediation

### Simple explanation and real-world example

A fix should make an observed weakness match a clear security requirement. Verification shows the repaired behavior still meets operational needs.

### Technical explanation

Remediation is the action taken to correct a weakness. The baseline records the original state. A retest compares the fixed state against the intended policy.

### Demonstration

Use a fictional shared folder with this intended rule: regular members can read, only editors can write, and outside accounts have no access. Its current policy grants all three groups write access.

### Hands-on exercise

Document the three before states and propose corrected access for each role. For each expected permission, state a safe verification result using test accounts or sample results.

### Expected result

Your after-state should allow regular members to read, editors to write, and outsiders neither. Include a check that legitimate access still works.

### Knowledge check

1. What is a baseline?
2. What does remediation correct?
3. Why verify allowed behavior alongside denied behavior?

### Mini challenge

Add an auditor who should read only selected records and describe how you would verify that scope.

## L-046 — Build an incident timeline

### Simple explanation and real-world example

A timeline helps you see which event occurred before another. Logs from different systems may report the same moment in different time zones.

### Technical explanation

A timestamp records an event time. UTC is a common reference time. Correlation means connecting observations that may refer to the same activity. Closely timed events can still be unrelated.

### Demonstration

Use these fictional records: login success at 09:15 UTC, settings change at 13:16 UTC+04:00, and failed login at 09:12 UTC.

### Hands-on exercise

Normalize the timestamps to UTC, put them in order, and label the earliest event that needs review. Explain what you would need to link the records to one account.

### Expected result

The expected order is 09:12 failure, 09:15 success, and 09:16 settings change. Account ID or a reliable shared identifier would help establish the link.

### Knowledge check

1. Why normalize time zones?
2. Which event happened last?
3. What helps correlate events beyond timestamps?

### Mini challenge

Add an event recorded as 13:11 UTC+04:00 and explain where it belongs.
