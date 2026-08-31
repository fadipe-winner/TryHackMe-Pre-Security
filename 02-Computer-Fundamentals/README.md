# Module 2 — Core Networking, Virtualization & Cloud Fundamentals

This module covers the fundamentals of how clients communicate with servers, basic networking concepts, virtualization, and cloud computing. These concepts are important for understanding how modern systems communicate and where security vulnerabilities can occur.

## Client-Server Basics

Almost everything you do online follows the same basic pattern: a **client** asks for something, and a **server** answers.

- **Client** — the device making the request (your laptop, phone, browser).
- **Server** — the device holding the data/service and responding to requests.

<u>How a request actually gets there:</u>

- **DNS (Domain Name System)** — translates a human-readable domain name (like `tryhackme.com`) into the IP address the computer actually needs to find that server. Think of it as the internet's phonebook.
- **IP Address** — the unique numerical address identifying a device on a network, similar to a street address for a house.
- **Port** — a number that identifies *which service* on that server you want to talk to, since one server can run multiple services at once (e.g., port 80 for HTTP, port 443 for HTTPS). If the IP address is the building, the port is the specific door/apartment number.
- **Protocol** — the agreed-upon "rules of conversation" both sides follow so they understand each other (HTTP, HTTPS, FTP, etc.).
- **Network** — the overall system of connected devices that allows the client and server to actually exchange data with each other.

**HTTP vs HTTPS**
- **HTTP** — the protocol web browsers and servers use to communicate, but sent in plain text.
- **HTTPS** — the same thing, but encrypted, so data can't be easily read or tampered with while in transit. This is why the padlock icon in your browser matters — it means you're on HTTPS.

**Common commands used to interact with this layer:**
- `ping <domain>` — checks if a server is reachable and measures response time.
- `nslookup <domain>` or `dig <domain>` — looks up the IP address behind a domain name (DNS lookup).
- `curl <url>` — sends a request to a server directly from the terminal and shows the response.

Every step here — DNS lookup, connecting to the right port, using the right protocol — is also a potential attack surface, which is why this basic flow matters so much in security.

---

## Virtualization Basics

Virtualization means one physical computer can pretend to be several separate computers at once, each isolated from the others. Each of these separate, self-contained environments is called a **virtual machine (VM)**.

- This is how TryHackMe gives you a full Linux or Windows machine to practice on without needing a separate physical computer for every room.
- Companies use it to run multiple servers on one physical machine, saving cost and hardware.
- Security-wise, this isolation matters: if one VM gets compromised, it's (ideally) contained and doesn't automatically affect the others.

---

## Cloud Computing Fundamentals

Cloud computing solves a problem most of us run into without realizing it — like moving files off a single laptop into online storage so you can access them from anywhere. Instead of running an app on one computer in one location, the cloud lets you use computing resources over the internet, making everything easier to access and scale.

**Analogy:** it's like a memory card — you can pull it out of one phone and pop it into another, and your data goes with you. The cloud does the same thing, just over the internet instead of physically moving a card.

### Types of Cloud
- **Public Cloud** — used by startups and websites; the go-to choice for nearly every use case.
- **Private Cloud** — used by banks, healthcare, and government due to the need for greater control over their data.
- **Hybrid Cloud** — used by companies like e-commerce businesses to back up sensitive data while still getting the flexibility of the public cloud.

### Main Cloud Service Models
- **IaaS (Infrastructure as a Service)** — you manage the operating system yourself; the provider just gives you the raw infrastructure. Example: AWS.
- **PaaS (Platform as a Service)** — the provider manages the infrastructure *and* the OS, so you can focus on building and running your app. Example: Azure.
- **SaaS (Software as a Service)** — you use a complete, ready-made application over the internet, and the provider manages everything else. Examples: Gmail, Zoom, Microsoft 365. Your main responsibility here is keeping your own account secure.

### Characteristics of Cloud Computing
- **Scalability** — easy to scale up or down as your application's needs change.
- **On-demand self-service** — provision resources yourself, whenever needed.
- **Pay-for-what-you-use** — billed based on actual usage.
- **High availability** — minimal downtime.
- **Global access** — reachable from anywhere in the world.

### Basic Cloud Terminology
- **EC2 (Elastic Compute Cloud)** — a virtual computer/server in the cloud — basically like adding a new computer to your environment, except virtual.
- **Instance Type** — describes how powerful that virtual computer is (its specs).


