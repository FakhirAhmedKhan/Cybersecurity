# Part 06 — Data validation and security fundamentals

Lessons 36–42 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 36 | L-060 | 4 | CSV and JSON for security reports |
| 37 | L-061 | 4 | Error handling and testing for security scripts |
| 38 | L-022 | 5 | Confidentiality, integrity, and availability |
| 39 | L-023 | 5 | Authentication and authorization |
| 40 | L-024 | 5 | Encryption and hashing |
| 41 | L-025 | 5 | Malware, phishing, and social engineering |
| 42 | L-026 | 5 | Threats, vulnerabilities, and risk |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-060 — CSV and JSON for security reports

### Simple explanation and real-world example

JSON can represent nested data. CSV presents records in a table that spreadsheet programs can read.

### Technical explanation

A JSON object has keys and values. A CSV row contains delimited fields. The header gives the column names and establishes which fields appear in each row.

### Demonstration

json.loads reads the sample list. csv.DictWriter maps object keys to known columns, writes the header, then writes one row per record. StringIO keeps the sample in memory.

```python
import csv
import io
import json

events = json.loads('[{"account":"alice","status":"failed"}]')
output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=["account", "status"])
writer.writeheader()
writer.writerows(events)
print(output.getvalue())
```

### Hands-on exercise

Run the example. Count the output data rows excluding the header, then add a second input object and compare counts.

### Expected result

The first version has the header account,status and one data row. The second version should have two data rows.

### Knowledge check

1. When is CSV useful?
2. What is the header?
3. Why count rows excluding the header?

### Mini challenge

Add a timestamp column and explain the change required in both the input and the field list.

## L-061 — Error handling and testing for security scripts

### Simple explanation and real-world example

A script should help you distinguish missing data from a valid file that happens to contain no events.

### Technical explanation

An exception signals an error while the code runs. Validate data after reading it. An empty valid input and an unreadable input have different meanings.

### Demonstration

The function below uses Path.read_text to read a local file, catches a specific FileNotFoundError, checks for an empty sample, and validates every record against the exercise’s two allowed values.

```python
from pathlib import Path

def check_log(path):
    try:
        lines = path.read_text(encoding="utf-8").splitlines()
    except FileNotFoundError:
        return "missing file"
    if not lines:
        return "empty file"
    if any(line not in {"OK", "FAILED"} for line in lines):
        return "malformed record"
    return "valid input"

print(check_log(Path("check.log")))
```

### Hands-on exercise

Try the example with a missing check.log, then create an empty one, then try it with INVALID and with OK. Restore the practice file between trials.

### Expected result

You should see missing file, empty file, malformed record, and valid input in the corresponding trials. Each message points to a different next step.

### Knowledge check

1. Why catch a specific exception?
2. Why distinguish empty input from missing input?
3. What evidence establishes the sample format is valid?

### Mini challenge

Add an explicit check that rejects whitespace-only records mixed into otherwise valid input.

## L-022 — Confidentiality, integrity, and availability

### Simple explanation and real-world example

The three CIA goals help you describe what a security problem actually harmed. An incident can affect more than one goal.

### Technical explanation

Confidentiality concerns who can read information. Integrity concerns unauthorized changes and accuracy. Availability concerns whether authorized users can access a service or its information.

### Demonstration

In a fictional clinic, a third party reads patient notes, a system records the wrong appointment time, and a power loss makes scheduling unavailable.

### Hands-on exercise

Classify those three events and write one sentence explaining each. Then consider a single incident that affects two goals.

### Expected result

The examples map to confidentiality, integrity, and availability, in that order. Your combined incident should explain two distinct effects.

### Knowledge check

1. Which goal protects private records?
2. What goal is affected by the changed appointment?
3. Can one incident affect all three?

### Mini challenge

Classify an outage that also causes a system to lose several saved updates.

## L-023 — Authentication and authorization

### Simple explanation and real-world example

When you sign in, a system checks who you are. When you ask for a record, it checks if you may see it.

### Technical explanation

Authentication establishes identity. Authorization evaluates an identity’s permissions for an action and resource. An access matrix lists allowed actions for each role.

### Demonstration

In a fictional school app, students may see their own results. Teachers may see results for assigned classes. An authenticated student requests another student’s results.

### Hands-on exercise

Create an access matrix for two roles and three actions: view own results, view assigned class results, and change grades. State the assumptions you made.

### Expected result

Your table includes explicit allow or deny decisions. Signing in by itself does not grant permission to read another student’s record.

### Knowledge check

1. What does authentication establish?
2. What does authorization check?
3. Why check permission on each protected record?

### Mini challenge

Add a substitute teacher and define how access ends after the assignment.

## L-024 — Encryption and hashing

### Simple explanation and real-world example

Encryption protects readable data by scrambling it with a key. Hashing helps you recognize whether data matches a known value.

### Technical explanation

Encryption uses a cryptographic key and produces ciphertext. Decryption recovers the readable data with the appropriate key. A hash produces a fixed-length value, or digest, from the input.

### Demonstration

Use your Lesson 1 file: calculating its hash gives a digest you can compare later. In a separate example, an encrypted backup can be restored with the correct key.

### Hands-on exercise

Fill out a two-row table. Choose encryption or hashing for a private backup and a check against a trusted file baseline, then explain each choice.

### Expected result

Select encryption for keeping the backup confidential and hashing for comparing the file contents. A private backup still needs controlled key access.

### Knowledge check

1. What is ciphertext?
2. What is a digest?
3. Which tool lets you recover the original data with a key?

### Mini challenge

Describe why both techniques can be useful for the same backup.

### References

- [NIST Secure Hash Standard · SHA-256](https://csrc.nist.gov/files/pubs/fips/180-4/final/docs/fips180-4.pdf)

## L-025 — Malware, phishing, and social engineering

### Simple explanation and real-world example

A message can pressure someone to act before they verify the request. A file attached to it may contain harmful software.

### Technical explanation

Phishing is deceptive communication intended to collect information or prompt a harmful action. Social engineering manipulates people. Malware is software designed to cause harm or unauthorized activity.

### Demonstration

Read this fictional email: “Your payroll access expires in 10 minutes. Reply with your password and open the attached update.” Work from this text alone.

### Hands-on exercise

Identify three clues, explain what the sender wants, and write how you would verify the claim through a known workplace channel.

### Expected result

Your record should name the time pressure, the password request, and the unverified attachment. The verification method should be independent of the message.

### Knowledge check

1. What is social engineering?
2. What makes a message phishing?
3. What does malware refer to?

### Mini challenge

Write a two-sentence internal report about the message using only the details you can confirm.

## L-026 — Threats, vulnerabilities, and risk

### Simple explanation and real-world example

A weakness matters when something can take advantage of it and the consequences are meaningful. The same weakness can have different urgency in different places.

### Technical explanation

A vulnerability is a weakness. A threat is a potential cause of harm. Risk considers likelihood and impact in context. An asset is something valuable that needs protection.

### Demonstration

Two fictional teams use an outdated library. One tool runs offline with dummy data. The other is an internet-facing app that holds customer records.

### Hands-on exercise

Compare the two cases using four headings: asset, vulnerability, possible threat, and impact. Write what extra facts you would check before assigning priority.

### Expected result

Your analysis should account for how reachable the software is and what data it holds. Version alone gives an incomplete risk picture.

### Knowledge check

1. What is the weakness in the example?
2. What affects likelihood?
3. Why does the type of data matter?

### Mini challenge

Add a safeguard that reduces likelihood in one case and describe its effect without assuming all risk is gone.
