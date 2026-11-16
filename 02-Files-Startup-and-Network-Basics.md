# Part 02 — Files, startup, and network basics

Lessons 8–14 in study order. Use the lesson ID to find the matching row in your tracker.

| Study order | Tracker ID | Phase | Lesson |
|---:|---|---:|---|
| 8 | L-051 | 1 | File extensions and Windows executable files |
| 9 | L-052 | 1 | Windows startup apps and background processes |
| 10 | L-006 | 2 | IP and MAC addresses |
| 11 | L-007 | 2 | DNS and DHCP |
| 12 | L-008 | 2 | TCP, UDP, ports, and protocols |
| 13 | L-009 | 2 | HTTP and HTTPS |
| 14 | L-010 | 2 | Routers, firewalls, and the internet |

Complete one practice task at a time. Write your prediction before doing the task, then compare your observation with the expected result. Save your answers and mini-challenge result under the matching tracker ID.

## L-051 — File extensions and Windows executable files

### Simple explanation and real-world example

Files with similar names can behave differently. Windows may hide the last part of a filename until you enable extensions.

### Technical explanation

A file extension is the suffix after the final dot, such as .txt. A shortcut usually points to another file or location. An executable contains instructions the system can run. An extension alone gives limited evidence about the actual contents.

### Demonstration

In File Explorer, enable file name extensions under View. Open Properties on a text file and a shortcut you already recognize.

### Hands-on exercise

Compare the full names and Properties of a text document, a trusted shortcut, and a Windows application you already know. Record each extension and its function.

### Expected result

The examples should have visibly different file types, such as .txt, .lnk, and .exe. Some apps may appear as shortcuts in File Explorer.

### Knowledge check

1. What does a shortcut contain?
2. Where is the extension in invoice.pdf.txt?
3. Why inspect Properties?

### Mini challenge

Explain what you would verify if a file’s icon and extension suggested different types.

## L-052 — Windows startup apps and background processes

### Simple explanation and real-world example

Some apps launch automatically when you sign in. Others run in the background with no window.

### Technical explanation

A startup app is configured to launch at sign-in. A background process performs work without a foreground window. These categories can overlap.

### Demonstration

Open Task Manager, look at Startup apps, and then look at Processes. Pick an entry you recognize in each view and use the available menu or file properties to identify its publisher.

### Hands-on exercise

Record one startup entry and one background process. Write the purpose of each and a piece of evidence, such as its publisher or file location.

### Expected result

You should be able to justify your choices without assuming an unfamiliar name is harmful.

### Knowledge check

1. When does a startup app launch?
2. Can a background process have no visible window?
3. What evidence helps identify the software?

### Mini challenge

Pick two startup entries and explain which one you would investigate first and why.

## L-006 — IP and MAC addresses

### Simple explanation and real-world example

Your laptop can have both a local network address and an adapter identifier. Think of the first as a delivery address and the second as a label used at the local delivery point.

### Technical explanation

An IP address identifies a network interface for IP communication. A MAC address identifies an interface for local link-layer communication. Devices can have several interfaces, and some platforms randomize MAC addresses.

### Demonstration

On Windows, ipconfig /all shows detailed network settings. Find your active Wi-Fi or Ethernet adapter, then look for IPv4 Address and Physical Address.

```powershell
ipconfig /all
```

### Hands-on exercise

Identify each address on your own adapter and record which one describes local-link delivery and which one describes IP delivery.

### Expected result

An IPv4 address looks like four numbers separated by dots. The physical address usually appears as six hexadecimal pairs on Windows.

### Knowledge check

1. What work does the IP address support?
2. What does Physical Address usually mean in ipconfig?
3. Why can one device show several addresses?

### Mini challenge

Find a disabled or disconnected adapter in the output and explain why you selected a different adapter.

## L-007 — DNS and DHCP

### Simple explanation and real-world example

DNS looks up names like a directory. DHCP can give a device its network settings when it joins Wi-Fi.

### Technical explanation

DNS resolves names into records, including IP addresses. DHCP leases IP configuration, often including a default gateway and DNS servers. A lease is temporary and can be renewed.

### Demonstration

ipconfig /all shows whether DHCP is enabled and lists any DNS servers. Resolve-DnsName asks your configured resolver for records for a normal public example domain.

```powershell
ipconfig /all
Resolve-DnsName example.com
```

### Hands-on exercise

Compare the DHCP and DNS fields for your active adapter, then run the lookup and identify which output describes your computer and which describes the domain.

### Expected result

The lookup should show one or more records if the name resolves. A network can use a manually configured IP while still using DNS.

### Knowledge check

1. Which service answers a name lookup?
2. Which service can assign device settings?
3. What might fail if DNS stops working?

### Mini challenge

Explain why a device might still communicate with a known IP address during a DNS outage.

## L-008 — TCP, UDP, ports, and protocols

### Simple explanation and real-world example

Different applications share a network connection. A port number helps the receiving system deliver traffic to the right service.

### Technical explanation

TCP provides an ordered, reliable byte stream. UDP sends individual messages, called datagrams, without built-in guarantees of delivery or ordering. A port identifies a transport endpoint within an IP address and protocol.

### Demonstration

Read these fictional capture entries: TCP 192.0.2.10:55000 → 192.0.2.20:443 and UDP 192.0.2.10:53121 → 192.0.2.53:53. Each entry shows protocol, source, and destination.

### Hands-on exercise

Label source and destination ports in each entry, then name one type of app that benefits from each transport.

### Expected result

You should identify 443 and 53 as the destination ports shown. The numbers suggest common services, and the capture or application context confirms what was used.

### Knowledge check

1. Which transport offers ordered delivery?
2. Why does a port matter?
3. Can a protocol number alone establish the application’s identity?

### Mini challenge

Explain what changes in the source and destination fields when the UDP reply comes back.

## L-009 — HTTP and HTTPS

### Simple explanation and real-world example

When you request a web page, the browser sends a message and the server responds. HTTPS protects those messages in transit.

### Technical explanation

HTTP defines request methods, headers, response status, and message bodies. HTTPS uses TLS to encrypt traffic and verify the server’s identity through its certificate under normal browser validation.

### Demonstration

Read this fictional exchange: request GET /notes, response 200 OK, Content-Type text/plain, body hello. GET asks to retrieve a resource, 200 indicates success, and Content-Type describes the body.

### Hands-on exercise

Label the method, path, status code, header, and body. Then describe which parts of the exchange the encrypted connection protects between endpoints.

### Expected result

You should label each component and explain that the browser and server can still read the contents locally.

### Knowledge check

1. Who sends an HTTP request?
2. What does 200 indicate?
3. What protection does TLS provide in transit?

### Mini challenge

Write a fictional response for a requested page that does not exist and explain what its status means.

## L-010 — Routers, firewalls, and the internet

### Simple explanation and real-world example

To visit a site elsewhere, your computer normally sends network traffic to a router that forwards it onward. A firewall can apply traffic rules along the way.

### Technical explanation

A router forwards packets between networks. A default gateway is the route a device commonly uses for destinations outside its local network. A firewall allows or blocks traffic according to policy.

### Demonstration

Sketch Laptop → Home router → Internet → Web server. Add an arrow for the reply and mark the router as the laptop’s default gateway for this example.

### Hands-on exercise

Draw the route in a small diagram and write one fictional firewall rule that permits ordinary web traffic from the laptop to the lab server.

### Expected result

Your diagram should show where packets leave the local network and where a rule evaluates traffic. The same device can perform routing and firewall functions.

### Knowledge check

1. What is a router’s job?
2. When does the default gateway matter?
3. What does a firewall rule decide?

### Mini challenge

Add a second device on the same local network and explain why its local traffic might take a different path.
