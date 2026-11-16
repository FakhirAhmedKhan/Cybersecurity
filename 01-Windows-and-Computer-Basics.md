# Part 01 — Windows and computer basics

Lessons 1–7 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 1 | L-001 | 1 | What Is Cybersecurity? |
| 2 | L-002 | 1 | How a computer runs a program |
| 3 | L-003 | 1 | Hardware, software, and the operating system |
| 4 | L-004 | 1 | Windows and Linux basics |
| 5 | L-005 | 1 | Files, folders, and PowerShell basics |
| 6 | L-040 | 1 | Windows security and account basics |
| 7 | L-050 | 1 | Windows Event Viewer basics |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

**Your progress:** The guided SHA-256 lab in L-001 passed. Pick up at its hands-on exercise to finish the file-restoration challenge, then do the knowledge check. The 70-lesson plan includes L-049, which was presented as optional in the tracker.

## L-001 — What Is Cybersecurity?

### Simple explanation and real-world example

Cybersecurity protects devices, applications, networks, and their information. A banking app should keep balances private, record amounts correctly, and open when you need it.

### Technical explanation

Confidentiality limits who can read data, integrity keeps data accurate and protects it from unauthorized changes, and availability keeps services usable. A SHA-256 hash is a 64-character hexadecimal value calculated from file contents. Compare it with a trusted baseline, which is a known-good earlier value.

### Demonstration

Your completed demo changed AED 50 to AED 500 and produced different hashes. In the original PowerShell window, Set-Content writes the original text to your practice file and Get-FileHash recalculates it. The -eq operator compares two values. If the old window is closed, recreate the baseline on a new temporary file before making and reversing the edit.

If `$file` and `$before` are still available, go straight to the hands-on exercise. Otherwise, run the baseline demo below. New-TemporaryFile creates a new file, Set-Content writes the practice text, and Get-FileHash computes a SHA-256 digest. The variables remember the file and original hash.

```powershell
$file = New-TemporaryFile
Set-Content -LiteralPath $file.FullName -Value "Payment amount: AED 50"
$before = (Get-FileHash -LiteralPath $file.FullName -Algorithm SHA256).Hash
Set-Content -LiteralPath $file.FullName -Value "Payment amount: AED 500"
```

### Hands-on exercise

Predict the result, restore the exact original text, then calculate a third hash. If you rebuilt the lab, compare against the baseline from that same session.

### Expected result

The restored file should match the baseline if its bytes match, including spaces, encoding, and the end of the line. A mismatch alone says nothing about who made a change.

### Knowledge check

1. Which goal protects private balances?
2. Which goal fails during an outage?
3. What does a different hash show?
4. What evidence could identify who changed the file?

### Mini challenge

Predict what happens if you add one trailing space to the restored text, then test it on the temporary file.

### References

- [PowerShell Get-FileHash reference](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-5.1)
- [NIST security objectives glossary](https://csrc.nist.gov/glossary/term/security_objective)

## L-002 — How a computer runs a program

### Simple explanation and real-world example

Think of opening Calculator. The app is stored on disk, and Windows gives the running app space to work in memory.

### Technical explanation

An executable contains program instructions. A process is a running instance with a process ID, or PID. RAM holds working data while the program runs. Storage keeps files when power is off.

### Demonstration

Open Task Manager with Ctrl+Shift+Esc and look at Processes. Open Calculator from Start and find its row. The Memory column shows how much memory the app is using as displayed by Task Manager.

### Hands-on exercise

Record Calculator’s displayed memory while it is open, close it normally, and observe what changes in Task Manager.

### Expected result

Calculator should become visible after launch. Its process may disappear or linger briefly after closing. The installed app stays on disk.

### Knowledge check

1. What is a process?
2. Where do unsaved working values usually live?
3. What happens to the installed app when you close it?

### Mini challenge

Find another app that uses multiple processes and explain why grouping helps you read the list.

## L-003 — Hardware, software, and the operating system

### Simple explanation and real-world example

Your computer contains physical parts and instructions. The processor executes instructions, memory holds what it needs now, and storage keeps files.

### Technical explanation

Hardware is physical. Software comprises instructions and data. The operating system manages access to the processor, memory, storage, and devices on behalf of running programs.

### Demonstration

In Windows Task Manager, open Performance and inspect the CPU, Memory, and Disk sections. The CPU graph measures activity. The Memory panel shows installed capacity and current usage.

### Hands-on exercise

Write down one detail from each of the three sections and match it to what that component does when you open a large PDF.

### Expected result

You should be able to identify three different measurements. A large disk capacity alone tells you little about how much RAM is free.

### Knowledge check

1. Which component executes instructions?
2. What survives a restart?
3. Who coordinates access to devices?

### Mini challenge

Explain how many open browser tabs can slow a laptop that still has plenty of free disk space.

## L-004 — Windows and Linux basics

### Simple explanation and real-world example

Windows and Linux both let you open files, run programs, and manage devices. Their default interfaces and directory conventions differ.

### Technical explanation

Windows typically uses drive letters such as C:. Linux presents a directory tree starting at /. A home directory is a user’s personal workspace. An account gives the operating system an identity for applying permissions.

### Demonstration

Compare the example personal paths C:\Users\Student\Documents and /home/student/Documents. Both point to documents under a user’s home. The Windows example begins with a drive letter and the Linux path begins at the root directory.

### Hands-on exercise

Make a two-column map of where a user keeps documents, finds settings, and runs commands in Windows and Ubuntu. Use an existing Ubuntu lab or the example paths.

### Expected result

Your map should connect each task across both systems even where folder names, path separators, and tools differ.

### Knowledge check

1. What is a home directory?
2. What does / mean at the start of a Linux path?
3. What job do both operating systems perform?

### Mini challenge

Explain what a path should look like for a Windows file and an Ubuntu file with the same name.

## L-005 — Files, folders, and PowerShell basics

### Simple explanation and real-world example

PowerShell lets you tell Windows which folder to inspect and which file to read.

### Technical explanation

The working directory is your shell’s current folder. A relative path starts from that folder. An absolute path identifies a location independently of your current folder.

### Demonstration

Get-Location prints your current folder. Get-ChildItem lists its contents. Get-Content reads a text file. The prefix .\ means the current folder.

```powershell
Get-Location
Get-ChildItem
Get-Content -LiteralPath .\notes.txt
```

### Hands-on exercise

In File Explorer, make notes.txt in a folder you own and open PowerShell in that folder. Run the example, then compare the shell output with File Explorer.

### Expected result

The current path should match your folder. The file listing should include notes.txt and Get-Content should print what you typed.

### Knowledge check

1. What is a working directory?
2. What does .\ mean?
3. Which command reads a text file?

### Mini challenge

Read notes.txt from its parent folder using a relative path.

### References

- [Microsoft Getting Started with PowerShell](https://github.com/MicrosoftDocs/PowerShell-Docs/blob/main/reference/docs-conceptual/learn/ps101/01-getting-started.md)

## L-040 — Windows security and account basics

### Simple explanation and real-world example

A standard Windows account can use most apps. Administrative privileges allow system-wide changes, such as installing a driver.

### Technical explanation

A privilege is permission to perform a system action. User Account Control, or UAC, asks for consent or administrator credentials when a program requests elevated access, depending on the account and settings.

### Demonstration

Compare editing your personal notes with changing a security setting for all users. The second affects the system and can trigger elevation.

### Hands-on exercise

For a fictional shared computer, classify editing your own file, installing a system driver, and viewing another person’s private folder. Record the expected access decision for each.

### Expected result

Your list separates ordinary user work from system-wide actions and access to another user’s data. Administrative access should have a specific reason.

### Knowledge check

1. What is elevation?
2. Why use a standard account for routine work?
3. What should you check before approving a UAC prompt?

### Mini challenge

Write a one-sentence access rule for a student account on a shared laptop.

## L-050 — Windows Event Viewer basics

### Simple explanation and real-world example

Event Viewer is Windows’ record book. It can tell you that a service started or that something failed, with a time and a source.

### Technical explanation

An event log stores records from the operating system and applications. The event ID identifies an event type within its source or provider. Read the source and message alongside the number.

### Demonstration

Open Event Viewer from Start, expand Windows Logs, and open System. Select an Information event and look at its General pane.

### Hands-on exercise

Record one event’s timestamp, source, ID, and main message in your own words. Use a routine event from your PC.

### Expected result

You should capture four details about one routine event. An informational entry often records ordinary activity.

### Knowledge check

1. What does the event source identify?
2. Why record the timestamp?
3. What else do you need besides an event ID?

### Mini challenge

Find a second event from the same source and compare the message with the first one.
