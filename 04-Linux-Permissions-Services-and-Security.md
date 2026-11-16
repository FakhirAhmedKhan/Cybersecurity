# Part 04 — Linux permissions, services, and security

Lessons 22–28 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 22 | L-014 | 3 | Users, groups, and permissions |
| 23 | L-015 | 3 | Linux processes and services |
| 24 | L-016 | 3 | Bash scripting basics |
| 25 | L-017 | 3 | Linux security fundamentals |
| 26 | L-042 | 3 | Keeping an Ubuntu lab isolated |
| 27 | L-056 | 3 | Package management and security updates |
| 28 | L-057 | 3 | Linux logs and journalctl |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-014 — Users, groups, and permissions

### Simple explanation and real-world example

You can let yourself edit a file while preventing other accounts from reading it. Permissions define those rules.

### Technical explanation

Linux lists permissions for the owner, group, and others. The letters r, w, and x mean read, write, and execute. On directories, x lets an allowed account pass through or access known names inside.

### Demonstration

In the previous lab folder, ls -l shows details about a file. chmod u=rw,go= grants the owner read and write access and removes permissions for the group and others.

```bash
ls -l course-files-lab/original.txt
chmod u=rw,go= course-files-lab/original.txt
ls -l course-files-lab/original.txt
```

### Hands-on exercise

Inspect original.txt, change its permissions, and inspect it again. Work on the practice file you own.

### Expected result

The mode should begin -rw------- after the change, followed by the other file details. The file contents should be intact.

### Knowledge check

1. What are the three permission groups?
2. What does w grant on a file?
3. What does x mean on a directory?

### Mini challenge

Write the permission change you would make to let only the owner and group read the file while keeping editing exclusive to the owner.

## L-015 — Linux processes and services

### Simple explanation and real-world example

Linux runs programs you open and background services that do work for the system.

### Technical explanation

A process is a running program instance. A service is a managed background function. On Ubuntu systems using systemd, systemctl reports service state.

### Demonstration

ps lists processes associated with your terminal. systemctl lists loaded service units with the requested state. The --no-pager option prints directly to the terminal.

```bash
ps
systemctl list-units --type=service --state=running --no-pager
```

### Hands-on exercise

Run these read-only commands on your own Ubuntu VM and record one interactive process and one running service.

### Expected result

ps typically shows your shell and the ps command. The service list varies. A minimal environment without systemd may report that it cannot connect to the service manager.

### Knowledge check

1. What distinguishes a service from the shell process?
2. What does the running filter do?
3. Why can a service have multiple processes?

### Mini challenge

Inspect a second service in the list and explain what other information you would need to identify its role.

## L-016 — Bash scripting basics

### Simple explanation and real-world example

A Bash script makes a task repeatable. For example, it can count how many lines in a practice log contain a failed sign-in marker.

### Technical explanation

A script stores commands in a text file. Bash executes them in order. grep searches for lines containing a pattern, and -c reports how many lines matched.

### Demonstration

Create demo.log in your own lab folder with three separate lines: LOGIN_OK alice, LOGIN_FAILED bob, and LOGIN_FAILED chris. Save the two lines below as count-failures.sh in the same folder. The first names Bash and the second counts matching lines.

```bash
#!/usr/bin/env bash
grep -c 'LOGIN_FAILED' demo.log
```

### Hands-on exercise

Run the script by typing bash count-failures.sh in that folder. Add another success line to the log and repeat the command.

### Expected result

Both runs should print 2 because the extra line does not include LOGIN_FAILED. grep prints the number of matching lines, so two occurrences on one line still count as one.

### Knowledge check

1. What does grep search?
2. What changes when -c is used?
3. Why put the commands in a script?

### Mini challenge

Modify the script to separately display counts for failed and successful sign-ins.

### References

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.pdf)

## L-017 — Linux security fundamentals

### Simple explanation and real-world example

A Linux lab is easier to protect when each user and service has only the access it needs.

### Technical explanation

Least privilege means granting the minimum permissions needed for a job. An access review compares actual permissions with an intended policy.

### Demonstration

Consider this fictional policy: the owner may edit a configuration, the service group may read it, and all other users should have no access. In the example the mode is 666, which gives everyone read and write access.

### Hands-on exercise

Write down which permissions conflict with the policy and propose a replacement mode. Read, write, and execute have values 4, 2, and 1 when writing the numeric mode.

### Expected result

The intended numeric mode is 640. The owner gets read and write, the group gets read, and others get no permissions.

### Knowledge check

1. What does least privilege mean?
2. Why review the desired policy first?
3. Who can write under mode 640?

### Mini challenge

Explain how you would verify the service can still read the configuration after the change.

## L-042 — Keeping an Ubuntu lab isolated

### Simple explanation and real-world example

A virtual machine is a computer running inside your computer. Separating its network and folders makes practice easier to control.

### Technical explanation

The host is your physical machine and its operating system. The guest is the virtual machine. A bridged adapter usually puts the guest on the surrounding network. An internal network can connect selected guests without exposing them to the surrounding network by default.

### Demonstration

Sketch a host, two training guests, and your home network. Draw an internal-network link between guests. Mark any shared folders or extra network adapters individually.

### Hands-on exercise

Draw your planned lab boundaries. Identify which connections and files you intend to share. Use the VM settings as evidence if the lab already exists.

### Expected result

Your diagram should make it easy to identify what can reach each guest. An extra bridged or NAT adapter can alter the network boundary.

### Knowledge check

1. What is the guest?
2. What does a shared folder expose?
3. How can a second network adapter affect isolation?

### Mini challenge

Review a fictional VM with an internal adapter and a bridged adapter. Mark which path connects it to the surrounding network.

## L-056 — Package management and security updates

### Simple explanation and real-world example

Linux applications and system components are often installed as packages. A package update can include bug fixes and security fixes.

### Technical explanation

A package manager tracks installed software and versions. A package repository supplies package metadata. APT uses local package lists to report which versions can be upgraded.

### Demonstration

On Ubuntu, apt list --upgradable displays packages with newer versions in the currently available package metadata. It reads the current state and does not apply updates.

```bash
apt list --upgradable
```

### Hands-on exercise

Run the read-only command on your Ubuntu VM. Pick one package and record the available and installed versions if listed.

### Expected result

You may see several entries or just a heading. An empty list reflects the metadata available on that VM and may change when package indexes are refreshed.

### Knowledge check

1. What does a package manager track?
2. What does an upgradable package mean?
3. Why do package lists need to be current?

### Mini challenge

Find the publisher’s change description for one package already familiar to you and classify the update it describes.

## L-057 — Linux logs and journalctl

### Simple explanation and real-world example

Linux service logs can tell you whether something started normally and when a problem first appeared.

### Technical explanation

The systemd journal collects event messages. journalctl reads the journal. A unit is the name systemd uses to identify a configured service or other managed item.

### Demonstration

On an Ubuntu VM using systemd, journalctl -b reads the current boot, -n 5 selects the five latest available entries, and --no-pager displays them directly. The messages you can see depend on your account’s permissions.

```bash
journalctl -b -n 5 --no-pager
```

### Hands-on exercise

Run the command and pick one routine entry. Record its timestamp, source, and event message, or note if your account has limited visibility.

### Expected result

You should see up to five available messages or a note about access. Exact timestamps and services depend on your VM.

### Knowledge check

1. What does -b select?
2. Why can user permissions affect log visibility?
3. Which field can connect entries from the same source?

### Mini challenge

Use a practice transcript to pick two events from the same source and put them in chronological order.
