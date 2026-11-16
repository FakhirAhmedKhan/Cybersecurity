# Part 07 — Account protection, cryptography, and network analysis

Lessons 43–49 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 43 | L-027 | 5 | Firewalls, antivirus, and monitoring |
| 44 | L-044 | 5 | Multifactor authentication and account recovery |
| 45 | L-045 | 5 | Backups and recovery |
| 46 | L-062 | 5 | Password storage, salts, and password hashing |
| 47 | L-063 | 5 | TLS certificates and browser trust |
| 48 | L-064 | 5 | Security patch prioritization |
| 49 | L-028 | 6 | Network analysis with Wireshark |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-027 — Firewalls, antivirus, and monitoring

### Simple explanation and real-world example

Security tools help in different ways. Some control traffic, some inspect files, and some record or flag events.

### Technical explanation

A firewall applies network policy. Antivirus or endpoint protection looks for harmful activity and may quarantine it. Monitoring collects observations. An alert prompts someone to investigate.

### Demonstration

Use three fictional events: blocked inbound traffic, a quarantined file, and an alert about repeated failed sign-ins. Associate each with the safeguard most directly involved.

### Hands-on exercise

Create a small incident timeline. For each event, label the relevant safeguard and whether the event shows prevention, detection, or evidence for follow-up.

### Expected result

You should associate the three events with a firewall, endpoint protection, and monitoring respectively. A single alert is a starting point for investigation.

### Knowledge check

1. Which control filters traffic?
2. What does quarantine mean?
3. Why review the evidence behind an alert?

### Mini challenge

Explain what you would want to know if monitoring reported a suspicious action without showing whether it was blocked.

## L-044 — Multifactor authentication and account recovery

### Simple explanation and real-world example

Multifactor authentication asks you to prove your identity in more than one way. Account recovery needs care because it can restore access when a factor is lost.

### Technical explanation

Factors commonly include something you know, have, or are. A password and a PIN are both knowledge factors. Recovery re-establishes access through a separately verified path.

### Demonstration

Model a fictional banking flow with a password and approval on a registered device. Draw a second path for replacing a lost device after identity verification.

### Hands-on exercise

Mark each factor type and circle the recovery step that should have a verification control. Add a notification to the existing account contact when recovery succeeds.

### Expected result

The password is knowledge. The registered device is possession. The recovery path should include an identity check and a record of the change.

### Knowledge check

1. What are the factor types in this example?
2. Why are a password and PIN one factor category?
3. Why does recovery deserve its own verification?

### Mini challenge

Identify what should happen to the old device’s access after it is replaced.

## L-045 — Backups and recovery

### Simple explanation and real-world example

A backup is a separate copy you can use when a file is lost or damaged. A restore proves you can get useful data back.

### Technical explanation

A backup captures data from a particular time. A restore recovers a chosen copy. Restoring to a new location avoids overwriting your current work during verification.

### Demonstration

In File Explorer, make a tiny practice text file with version A, copy it to a practice backup folder, then edit the original to version B.

### Hands-on exercise

Restore the backup copy to a different practice filename. Open it and compare its contents with your expected version.

### Expected result

The restored copy should contain version A while your current working file still contains version B. Which copy is newer depends on the intended restore point.

### Knowledge check

1. What is a restore point?
2. Why restore to a new location during practice?
3. Which goals are supported by a successful restore?

### Mini challenge

Explain which backup you would choose if the latest copy already contained a mistake.

## L-062 — Password storage, salts, and password hashing

### Simple explanation and real-world example

A service can verify a password using a stored result of a password-specific calculation. A unique salt makes identical passwords produce different stored results.

### Technical explanation

A salt is a unique value combined with the password and stored alongside the result. Password hashing should use a dedicated, tunable approach such as Argon2id. A work factor controls how costly each verification is.

### Demonstration

Draw two fictional accounts with the same placeholder password. Give each account a different salt and draw different stored outputs for the same password-hashing method.

### Hands-on exercise

Explain how the service uses a saved salt to check a later sign-in. Keep real passwords out of the exercise.

### Expected result

Your diagram shows different salts and stored results. Verification repeats the computation with the account’s saved parameters and compares results.

### Knowledge check

1. What does a salt do?
2. Why use a dedicated password-hashing method?
3. Which values are saved for later verification?

### Mini challenge

Explain how repeated use of the same salt across accounts would change your diagram.

### References

- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)

## L-063 — TLS certificates and browser trust

### Simple explanation and real-world example

A browser uses a certificate to check the site’s identity when it sets up HTTPS. A certificate must match the site and meet trust and date checks.

### Technical explanation

The hostname is the site name in the URL. The certificate’s Subject Alternative Name lists names it covers. A trust chain connects it to a certificate authority trusted by the browser. The validity period sets accepted dates.

### Demonstration

Assume today is 15 May 2027 and you request shop.example. Sample A covers shop.example and expires in July 2027, B covers shop.example and expired in April 2027, and C covers help.example and expires in July 2027. Assume the same valid trust chain for all three.

### Hands-on exercise

Classify each sample and write the precise field that supports the decision.

### Expected result

Under the exercise assumptions, A passes the listed checks, B is expired, and C has a name mismatch.

### Knowledge check

1. What identifies the requested site?
2. What does the expiration date test?
3. What does the trust chain establish?

### Mini challenge

Add a fourth fictional sample that matches the name and dates but fails trust-chain verification.

## L-064 — Security patch prioritization

### Simple explanation and real-world example

You rarely fix every software issue at once. Prioritize the cases where the affected software is present and the consequences are most serious.

### Technical explanation

An advisory identifies affected versions and discusses remedies. Exposure describes who or what can reach a component. Compensating controls reduce risk while a permanent fix is being prepared.

### Demonstration

Compare three fictional cases: an affected internet-facing service handling customer data, an affected internal reporting tool with limited access, and an advisory for a product absent from the inventory.

### Hands-on exercise

Rank the cases. For each, write why it belongs there and one fact you would verify before scheduling maintenance.

### Expected result

The exposed, affected customer service should generally rank first. The absent product needs inventory confirmation before closure. The internal tool still deserves review.

### Knowledge check

1. What does affected version mean?
2. Why examine internet exposure?
3. What does a compensating control do?

### Mini challenge

Change one fact about the internal tool that would raise its urgency and explain why.

## L-028 — Network analysis with Wireshark

### Simple explanation and real-world example

Wireshark shows captured network messages so you can see when devices spoke and what protocols they used.

### Technical explanation

A capture file stores packets from an observation point. A display filter changes which captured packets are visible. A DNS query asks for a record and a response replies to that query.

### Demonstration

Open an exercise PCAP or PCAPNG in Wireshark. Type dns in the display filter bar and press Enter. The filter shows packets Wireshark recognizes as DNS.

### Hands-on exercise

With a capture that contains ordinary DNS, pick one query and its reply. Record their frame numbers, timestamps, and queried name.

If you do not have a capture file, practice on this fictional packet list. The two DNS rows have the same transaction ID, which helps associate the reply with the query.

| Frame | Time (s) | Source | Destination | Details |
|---:|---:|---|---|---|
| 12 | 0.110 | 192.0.2.10 | 192.0.2.53 | DNS query 0x3142 for A record of shop.example |
| 13 | 0.113 | 192.0.2.53 | 192.0.2.10 | DNS response 0x3142 with A record 192.0.2.20 |
| 14 | 0.126 | 192.0.2.10 | 192.0.2.20 | TCP connection start |

### Expected result

You should identify a request and related response when both appear in the capture. Encrypted DNS may appear under a different protocol and the capture might omit a reply.

### Knowledge check

1. What does a capture store?
2. What does a display filter change?
3. What connects a DNS question with a reply?

### Mini challenge

Clear the filter and explain what happened to the number of visible packets and to the saved file.

### References

- [Wireshark User’s Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
