# Module 3 — Operating System Basics

In this module, I explored how operating systems work and practiced
interacting with both Windows and Linux environments.

Before going through this module, I mostly thought about an operating
system as the software that allows us to use a computer. I now understand
it more as the layer responsible for managing the computer's hardware,
applications, users, files, memory, processes, and other system resources.

For cybersecurity, this is important because a lot of activity that a
security analyst investigates happens on operating systems. Understanding
how a system normally works makes it easier to understand what is happening
when something unusual occurs.

---

## Understanding the Operating System

An Operating System (OS) is the core software that manages a computer's
hardware and provides an environment where applications can run.

Some of the major responsibilities of an operating system include:

- **Process Management** — creating, scheduling, prioritizing, and
  terminating running programs.
- **Memory Management** — allocating and managing RAM for processes.
- **File System Management** — organizing files and directories and
  controlling how they are accessed.
- **User Management** — managing user accounts, authentication, and
  permissions.
- **Device Management** — allowing the operating system to communicate
  with hardware through device drivers.

A simple way I understand it is:

**User → Application → Operating System → Hardware**

The operating system sits between applications and the underlying hardware,
managing access to the computer's resources.

---

## Kernel Space and User Space

One concept I found important was the separation between **kernel space**
and **user space**.

### Kernel Space

Kernel space is where the core part of the operating system runs. The
kernel has highly privileged access to system resources and is responsible
for important operations such as managing memory, processes, hardware, and
devices.

### User Space

User space is where normal applications usually run.

Applications have more restricted access to system resources than the
kernel. When an application needs something that requires privileged
system access, it relies on the operating system to perform that operation.

### Why This Matters for Security

This separation helps protect the operating system from applications
having unrestricted access to critical system resources.

It also helped me understand why **privileges matter so much in
cybersecurity**. What a user or process is allowed to do can determine how
much impact its actions can have on a system.

---

## GUI and CLI

I also learned more about the two common ways of interacting with an
operating system.

### Graphical User Interface (GUI)

A GUI provides a visual way of interacting with the computer through
windows, icons, menus, buttons, and other graphical elements.

This is how most people interact with desktop operating systems.

### Command-Line Interface (CLI)

A CLI allows a user to interact with the operating system using
text-based commands.

Instead of navigating through graphical menus, commands can be used to
navigate files, retrieve system information, manage resources, and perform
administrative tasks.

For security work, becoming comfortable with the CLI is particularly
useful because many tools and systems are operated through a terminal.

---

# Windows Basics

## Windows User Accounts and Authentication

I learned that Windows uses authentication to verify the identity of a
user before giving them access to the system.

Different accounts can have different levels of access.

Examples include:

- **Guest** — limited or temporary access.
- **Standard User** — intended for normal everyday tasks.
- **Administrator** — a privileged account capable of making significant
  changes to the system.

This introduced me to an important security principle: users should not
automatically have more privileges than they need.

If an account has unnecessary administrative privileges, activity
performed through that account can potentially have a much greater impact
on the system.

---

## Configuring Windows

I explored two common areas used to configure Windows:

### Windows Settings

The modern interface used to configure devices, accounts, networking,
security, applications, and other system settings.

### Control Panel

The traditional Windows management interface that still provides access
to many system configuration tools.

Understanding where system settings are managed is useful when checking
the configuration and security posture of a Windows endpoint.

---

## Task Manager

Task Manager gave me a practical view of what is currently happening on a
Windows system.

Some of the information available through Task Manager includes:

- **Processes** — applications and processes currently running.
- **Performance** — CPU, memory, disk, network, and other resource usage.
- **Users** — users currently logged into the system.
- **Services** — Windows services and their current state.

From a cybersecurity perspective, the **Processes** section stood out to
me.

If suspicious activity occurs on an endpoint, understanding processes can
help when trying to determine what programs are running and how the system
is behaving.

---

## Windows Security

I also explored some of the built-in security protections available in
Windows.

These include:

- Virus and threat protection
- Firewall and network protection
- App and browser controls
- Device security

### Windows Defender Firewall

A firewall helps control network traffic entering and leaving a system
based on defined rules.

This is important because not every network connection should automatically
be allowed.

For a security analyst, understanding host-based firewall protection is
useful when investigating network activity and checking whether security
controls are configured correctly.

---

# Linux CLI Basics

A major part of this module was becoming more comfortable using Linux
through the command line.

Rather than trying to memorize every command, I focused on understanding
what information each command helps me retrieve.

## Navigating the File System

### `pwd`

Displays the current working directory.

```bash
pwd
### `ls`

The `ls` command lists the files and directories in my current location.

```bash
ls
```

I also practiced using options with `ls` to get additional information.

```bash
ls -l
```

The `-l` option displays a detailed listing, including information such as
file permissions, ownership, size, and modification time.

To include hidden files:

```bash
ls -a
```

In Linux, files and directories whose names begin with a dot (`.`) are
normally hidden from a basic `ls` listing.

Both options can also be combined:

```bash
ls -la
```

This gives me a detailed listing that also includes hidden files.

#### Security Relevance

During an investigation, simply knowing that a file exists may not be
enough. Information such as its owner and permissions can provide
additional context, while viewing hidden files can reveal items that are
not shown in a normal directory listing.

---

### `cd`

The `cd` (change directory) command allows me to move between directories.

```bash
cd Documents
```

I can also move using an absolute path:

```bash
cd /var/log
```

To move up one level:

```bash
cd ..
```

To return to my home directory:

```bash
cd ~
```

Together, `pwd`, `ls`, and `cd` allow me to answer three basic questions
when working from the terminal:

- **Where am I?** → `pwd`
- **What's around me?** → `ls`
- **Where do I want to go?** → `cd`

---

## Reading and Finding Files

### `cat`

The `cat` command can be used to display the contents of a text file
directly in the terminal.

```bash
cat filename.txt
```

For example:

```bash
cat mission_brief.txt
```

This allows me to quickly inspect a file without opening it in a graphical
text editor.

---

### `find`

The `find` command can be used to search for files and directories.

A basic example is:

```bash
find /path -name "filename"
```

For example:

```bash
find /home -name "report.txt"
```

Here, `/home` is the location where the search begins, while `-name`
specifies the filename I am looking for.

#### Security Relevance

During an investigation, I may know the name of a file without knowing
where it is stored. Searching the filesystem from the command line can
help locate relevant files more efficiently.

---

## Gathering System Information

Knowing how to navigate a system is useful, but I also practiced gathering
basic information about the system I am working on.

### `whoami`

The `whoami` command displays the user account I am currently operating as.

```bash
whoami
```

I remember this simply as:

> **"Who am I logged in as?"**

This matters because different users can have different permissions and
privileges.

---

### `uname`

The `uname` command provides information about the operating system and
kernel.

```bash
uname -a
```

The `-a` option displays a broader set of available system information.

This can help me quickly understand the Linux environment I am working
with.

---

### `df`

The `df` command displays information about filesystem disk-space usage.

```bash
df -h
```

The `-h` option displays sizes in a more human-readable format.

This makes it easier to see how much storage is being used and how much
space remains available.

---

## Users and Remote Access

### `su`

The `su` command can be used to switch to another user account when the
appropriate authentication and permissions are available.

```bash
su - username
```

This reinforced something important for me: **the account I am operating
as determines what I may be allowed to access or modify.**

---

### SSH

SSH (Secure Shell) is used to securely access another system remotely
through the command line.

The general format is:

```bash
ssh username@host
```

Instead of putting the specific TryHackMe username and IP address from my
lab into this repository, I am documenting the general syntax.

SSH is important because many Linux servers are administered remotely
rather than through a physical keyboard and monitor.
## Key Takeaway

My biggest takeaway from this module is that understanding the operating
system is an important part of understanding security. I became more
comfortable navigating both Windows and Linux, using the command line,
gathering system information, and understanding users, processes,
permissions, and basic security controls.

These are still foundational skills, but they give me a better starting
point for investigating what is happening on a system as I progress
toward more SOC and Blue Team-focused learning.
