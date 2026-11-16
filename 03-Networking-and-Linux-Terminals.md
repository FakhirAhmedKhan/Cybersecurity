# Part 03 — Networking and Linux terminals

Lessons 15–21 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 15 | L-011 | 2 | Basic network troubleshooting |
| 16 | L-041 | 2 | Read a network troubleshooting transcript |
| 17 | L-053 | 2 | IPv4 subnet masks and CIDR |
| 18 | L-054 | 2 | Private IPs, public IPs, and NAT |
| 19 | L-055 | 2 | IPv6 and dual-stack networks |
| 20 | L-012 | 3 | Ubuntu and the Linux terminal |
| 21 | L-013 | 3 | Linux files and directories |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-011 — Basic network troubleshooting

### Simple explanation and real-world example

When a site won’t open, the issue may be your network connection, name lookup, or the application. Check one layer at a time.

### Technical explanation

A network interface connects the device to a network. A host name maps to an address through name resolution. Application status codes describe what the service returned after contact.

### Demonstration

In this fictional log, Wi-Fi is connected, the lab gateway responds, and the lab server responds by IP. The browser records name lookup failed for the hostname.

### Hands-on exercise

Write a three-line diagnosis. State which layer first shows a failure, which two checks succeeded, and one observation that would confirm the failure.

### Expected result

The evidence points toward name resolution. A working gateway by itself would provide weaker evidence than a successful connection to the same service by IP.

### Knowledge check

1. Why check one layer at a time?
2. Which result suggests a name-resolution problem?
3. What does an HTTP error imply about reaching a server?

### Mini challenge

Diagnose a second case where DNS resolves correctly and the server replies with a 503 status.

## L-041 — Read a network troubleshooting transcript

### Simple explanation and real-world example

Troubleshooting transcripts show the order in which checks were done. Read them like a timeline of evidence.

### Technical explanation

A baseline is the expected working state. An observation is what a test showed. A diagnosis explains which component most likely caused the symptom.

### Demonstration

Read this fictional transcript: adapter connected; local address present; DNS returns 192.0.2.20; server replied 403 Forbidden for /reports.

### Hands-on exercise

Mark the first unsuccessful step and quote the exact line that supports your diagnosis. Identify one thing that remains uncertain.

### Expected result

You should point to the application response as the first visible failure. The transcript supports an access denial without establishing its exact reason.

### Knowledge check

1. What is the first failure?
2. Which observation establishes name resolution worked?
3. What information could distinguish two causes of the 403?

### Mini challenge

Rewrite the transcript so the evidence points to loss of local network connectivity.

## L-053 — IPv4 subnet masks and CIDR

### Simple explanation and real-world example

A network mask tells devices which part of an IPv4 address identifies the local network.

### Technical explanation

CIDR writes the number of network bits after a slash. A /24 mask is 255.255.255.0. A /25 divides the final octet into ranges 0–127 and 128–255.

### Demonstration

With /24, 192.0.2.10 and 192.0.2.200 share a network. With /25, the same addresses fall in different halves of the final octet.

### Hands-on exercise

On paper, classify three pairs: 192.0.2.25 and 192.0.2.80 at /25, 192.0.2.100 and 192.0.2.130 at /25, and 192.0.2.25 and 192.0.3.25 at /24.

### Expected result

The outcomes in order are same, different, different. For each, show the address range or the octets that you compared.

### Knowledge check

1. What does /24 count?
2. Where does /25 split a /24?
3. Why can changing only the mask change your answer?

### Mini challenge

Determine which /26 range contains 192.0.2.150 and give its boundaries.

## L-054 — Private IPs, public IPs, and NAT

### Simple explanation and real-world example

Devices at home often have separate local addresses but reach the internet through the same router.

### Technical explanation

Private IPv4 ranges are intended for internal use. NAT means Network Address Translation. Many home routers also translate source ports so several internal connections can share one public address.

### Demonstration

Draw two clients, 192.168.1.10 and 192.168.1.11, using a router with a fictional public-facing address 198.51.100.10. Give each translated outgoing connection a different source port.

### Hands-on exercise

Draw the return arrows and explain how the router matches each reply to its originating device.

### Expected result

Your arrows use the router’s translation record to send each reply to the matching internal address and port.

### Knowledge check

1. Which address is private here?
2. What does NAT translate?
3. Why might the router track ports?

### Mini challenge

Explain why two people can report the same apparent internet address while using different laptops.

## L-055 — IPv6 and dual-stack networks

### Simple explanation and real-world example

Your computer can use two generations of the Internet Protocol side by side.

### Technical explanation

IPv4 addresses are 32 bits and commonly written in dotted decimal. IPv6 addresses are 128 bits and written in hexadecimal groups. Dual stack means a device or network supports both.

### Demonstration

Compare IPv4 example 192.0.2.8 with IPv6 example 2001:db8::8. In the IPv6 address, :: compresses an uninterrupted sequence of zero groups.

### Hands-on exercise

Classify these examples by version: 192.0.2.20, 2001:db8::20, and fe80::1. Expand 2001:db8::20 into eight groups.

### Expected result

Your expansion places five zero groups between 0db8 and 0020. The final two examples use IPv6 notation.

### Knowledge check

1. How many bits does IPv6 use?
2. What does :: represent?
3. What does dual stack mean?

### Mini challenge

Explain how the two versions can be present even if an app only uses one during a given connection.

## L-012 — Ubuntu and the Linux terminal

### Simple explanation and real-world example

The Ubuntu terminal lets you work with files and programs by typing instructions. It is useful for repeating an exact task or following a troubleshooting walkthrough.

### Technical explanation

A terminal is the window you type in. A shell interprets commands. Bash is a common Linux shell. The working directory is the folder it uses for relative paths.

### Demonstration

Open Terminal in Ubuntu. The pwd command prints your current directory, ls lists entries, and whoami prints your current username.

```bash
pwd
ls
whoami
```

### Hands-on exercise

Run the three commands and identify which value tells you the folder and which tells you the account.

### Expected result

A new terminal commonly starts in your home directory. The ls output depends on the files you have saved there.

### Knowledge check

1. What is a shell?
2. What information does pwd show?
3. What does whoami show?

### Mini challenge

Open a second terminal after navigating the first into a subfolder and predict where the second starts.

### References

- [Microsoft Ubuntu on Windows (WSL) install guide](https://github.com/MicrosoftDocs/wsl/blob/main/WSL/install.md)

## L-013 — Linux files and directories

### Simple explanation and real-world example

Linux directories organize files the same way folders organize notes on your computer.

### Technical explanation

The root directory is /. A parent directory contains the current directory. A leading dot in a filename hides it from ordinary ls output.

### Demonstration

In a fresh practice folder, mkdir creates a directory. printf writes formatted text and > sends it to a named file. cp copies a file. cat displays that file’s content.

```bash
mkdir course-files-lab
printf '%s\n' 'storage sample' > course-files-lab/original.txt
cp course-files-lab/original.txt course-files-lab/copy.txt
cat course-files-lab/copy.txt
```

### Hands-on exercise

Run these commands in your own home directory with an unused course-files-lab folder name. Compare the original and copy when you finish.

### Expected result

cat should print storage sample. You should have two files with the same contents and different names.

### Knowledge check

1. What does mkdir create?
2. What does > do?
3. What is the root directory?

### Mini challenge

Create a subdirectory under the lab folder and copy only the second file into it.
