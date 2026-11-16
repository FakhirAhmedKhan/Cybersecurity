# Part 05 — Python for cybersecurity

Lessons 29–35 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 29 | L-058 | 3 | sudo and least privilege |
| 30 | L-018 | 4 | Python fundamentals |
| 31 | L-019 | 4 | Scripting and automation |
| 32 | L-020 | 4 | Working with files and logs |
| 33 | L-021 | 4 | APIs and HTTP requests |
| 34 | L-043 | 4 | Summarize security events with Python |
| 35 | L-059 | 4 | Regular expressions for log parsing |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-058 — sudo and least privilege

### Simple explanation and real-world example

Some maintenance tasks need extra permissions. A person who checks service health may need different privileges from a person who administers accounts.

### Technical explanation

sudo runs a permitted command as another user, commonly root. Root is the administrator account. A least-privilege policy limits which accounts receive elevated access and for what purpose.

### Demonstration

Compare three fictional permissions: read a service status, restart one approved service, and run any command as root. Consider the scope of each action.

### Hands-on exercise

Assign an appropriate level of access to a help-desk worker, service operator, and system administrator in the example. Write a reason for each choice.

### Expected result

The help-desk role should have the smallest access needed. The service operator should be able to do the approved maintenance task. Broader authority needs a clear administrative reason.

### Knowledge check

1. What does sudo do?
2. Why distinguish reading status from restarting a service?
3. Who is root?

### Mini challenge

Review a fictional maintenance roster and identify a role whose access exceeds its duties.

## L-018 — Python fundamentals

### Simple explanation and real-world example

Python can count repeated events for you. You can begin with a list of outcomes from a fictional login system.

### Technical explanation

A variable names a value. A list holds ordered values. A loop repeats an operation for each value. An if statement runs its body only when its condition is true. A function gives reusable steps a name.

### Demonstration

The function below starts at zero and adds one for each item equal to failed. return gives the result back to the caller. print displays it.

```python
def count_failures(outcomes):
    count = 0
    for outcome in outcomes:
        if outcome == "failed":
            count += 1
    return count

print(count_failures(["ok", "failed", "failed"]))
```

### Hands-on exercise

Save the example as a local .py file and run it from your editor. Change one ok entry to failed and predict the new result first.

### Expected result

The example prints 2. After changing the single ok entry to failed it prints 3.

### Knowledge check

1. Where is the condition checked?
2. What does count hold?
3. What does return do?

### Mini challenge

Predict what the function does with an empty list and confirm your prediction.

## L-019 — Scripting and automation

### Simple explanation and real-world example

Automation is useful when you must do the same thing for several files. A short script can apply one calculation to every practice log.

### Technical explanation

A batch processes several inputs in one run. A glob is a filename pattern. Path.glob selects matching paths, sorted makes the processing order predictable, and read_text returns the file’s contents.

### Demonstration

Create a local study-logs folder with monday.log and tuesday.log. Put FAILED once in the first and twice on separate lines in the second. The script visits matching files and counts lines that exactly equal FAILED.

```python
from pathlib import Path

for path in sorted(Path("study-logs").glob("*.log")):
    lines = path.read_text(encoding="utf-8").splitlines()
    print(path.name, sum(line == "FAILED" for line in lines))
```

### Hands-on exercise

Run the example from the folder that contains study-logs. Add a third .log file and compare the outputs from both runs.

### Expected result

Initially you should see monday.log 1 and tuesday.log 2. The new file gets its own line after you add it.

### Knowledge check

1. What selects only .log files?
2. Why sort the paths?
3. What can you test before using the script on more files?

### Mini challenge

Add a text file with a .txt extension and predict whether it affects the output.

## L-020 — Working with files and logs

### Simple explanation and real-world example

A log is a list of recorded events. Reading one line at a time lets you count which events happened during a period.

### Technical explanation

A timestamp identifies when an event occurred. A text parser extracts meaningful fields. A context manager closes an open file after use. The strip method removes surrounding whitespace.

### Demonstration

Make a local demo.log containing separate lines 09:14 FAILED, 09:40 OK, and 10:01 FAILED. The example opens the file, removes line breaks at the ends, and counts entries ending with a space and FAILED.

```python
with open("demo.log", encoding="utf-8") as log:
    failures = sum(line.strip().endswith(" FAILED") for line in log)
print(failures)
```

### Hands-on exercise

Run the example and then change it to count only failed logins in the 09 hour. Use the timestamp as your selection criterion.

### Expected result

The first result is 2 and the filtered result should be 1. The script assumes the simple log layout used in this lesson.

### Knowledge check

1. What is a timestamp?
2. Why strip each line?
3. Why should a parser know the log format?

### Mini challenge

Add one unrelated text entry and explain whether the count should change.

## L-021 — APIs and HTTP requests

### Simple explanation and real-world example

An API gives software a defined way to ask another program for data. A local practice API might return your sample inventory.

### Technical explanation

A request has a method and path. A response has a status and a payload. JSON represents values in a structured format that Python can parse.

### Demonstration

Use a saved response body for this exercise. The example simulates a successful GET /assets response. json.loads converts the response text into Python values and the assets key returns a list.

```python
import json

status = 200
body = '{"assets": ["lab-server"]}'
data = json.loads(body)
print(status, len(data["assets"]))
```

### Hands-on exercise

Run the example and add a second fictional asset to the JSON text. Print the number of returned assets.

### Expected result

The original example prints 200 and 1. After adding a second member correctly, the count becomes 2.

### Knowledge check

1. What is a response status?
2. What does JSON provide?
3. What difference would a 404 make to your interpretation?

### Mini challenge

Write a response sample for an empty assets list and predict its count.

## L-043 — Summarize security events with Python

### Simple explanation and real-world example

A script can summarize repeated sign-in attempts into a table that a human can review.

### Technical explanation

A record represents one event. Aggregation counts or combines records. Counter groups values and tracks how often each occurs. A test fixture is a small set of input data with known results.

### Demonstration

The example counts fictional account and outcome pairs. Python’s tuple keeps each account together with its result, so alice with ok is a separate group from alice with failed.

```python
from collections import Counter

events = [("alice", "failed"), ("alice", "failed"), ("bob", "ok")]
print(dict(Counter(events)))
```

### Hands-on exercise

Run the code and check each count by hand. Try an empty list, then add a known record and compare again. In a later version, check the shape of each incoming record before counting it.

### Expected result

The example reports two alice failures and one bob success. An empty list produces an empty dictionary.

### Knowledge check

1. What is the grouping key?
2. Why compare with counts worked out by hand?
3. How would you handle incomplete records?

### Mini challenge

Modify the input and summarize outcomes by account without losing the distinction between ok and failed events.

## L-059 — Regular expressions for log parsing

### Simple explanation and real-world example

A regular expression is a rule for matching patterns in text. A log parser can use one to find fields that follow a known layout.

### Technical explanation

In Python regular expressions, the sequence \d matches a digit. Braces specify a repeat count. Parentheses capture part of a match. fullmatch requires the entire input to fit the pattern.

### Demonstration

Review the example pattern. It captures a time shaped like HH:MM, followed by one space and a three-digit status. The second line is missing the expected time shape.

```python
import re

pattern = r"(\d{2}:\d{2}) (\d{3})"
for line in ["09:15 200", "early 404"]:
    match = re.fullmatch(pattern, line)
    print(match.groups() if match else "malformed")
```

### Hands-on exercise

Run the example and try one more well-formed and one malformed input. Record which lines matched and which were rejected.

### Expected result

The first line produces a pair of strings, 09:15 and 200. The second prints malformed. A shape check alone does not prove a time is within a valid clock range.

### Knowledge check

1. What does \d{2} match?
2. Why use fullmatch here?
3. What validation would reject a time of 99:99?

### Mini challenge

Extend the rule to also capture the literal outcome word OK or FAILED at the end.
