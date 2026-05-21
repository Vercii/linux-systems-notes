# Module 2 - Operating Systems
An operating system (OS) is software that runs on a computing device and manages both hardware and software components to make the system functional.

Modern operating systems go beyond basic hardware control by also:
- Managing resources (CPU, memory, storage, devices)
- Scheduling processes so multiple programs can run in a multitasking way (sharing CPU time to appear simultaneous)
- Providing standard services that allow users and applications to request actions (e.g., printing a document), which the OS then executes

Operating systems vary in complexity depending on their purpose:
- Desktop and server OSs are generally complex and feature-rich
- Embedded or single-purpose systems (like firewalls, set-top boxes, or mobile devices) tend to be more specialized and limited in scope
- At the extreme, operating systems also run on supercomputers and large computing clusters

In general, the term operating system refers to the core software that boots and runs on a device, regardless of its scale or purpose.

The broader software stack acts as a bridge between users and hardware, and includes:
- System software
- Applications
- The operating system itself

## The Choices
Today, users mainly choose between three major operating systems:
- Microsoft Windows
- Apple macOS
- Linux

These systems differ in their underlying architecture:
- Windows
    - Uses a fully proprietary code base.
    - Is not based on UNIX or Linux systems.
- macOS
    - A certified UNIX-based operating system derived from BSD UNIX (pre-1995 lineage).
    - Includes significant proprietary Apple components.
    - Runs on Apple-optimized hardware.
- Linux
    - Not a single OS, but a family of distributions.
    - Built around the Linux kernel with GNU and other open-source components.
    - Can be customized for many purposes, from desktops to servers.
    
Despite differences under the hood, everyday user interaction is similar:
- All systems support GUI-based workflows (pointing, clicking, and standard productivity tasks).

Differences become more noticeable in system administration:
- Windows administration is mostly GUI-driven.
- Linux and UNIX-like systems often rely heavily on the command line interface (terminal) for powerful system management tasks.
- Knowledge of UNIX-style commands often transfers well between Linux and macOS.
- Many Windows administrative tools have command-line equivalents used for efficiency and automation.

## Decision Points
When selecting a computer system, the first consideration is its role:
- Desktop systems are used for personal productivity and browsing, typically with a GUI for ease of use.
- Server systems provide services to other users or systems and are usually accessed remotely, often using a CLI for efficiency and resource savings.

The function of the machine also matters:
- What software it must run
- How many machines are deployed
- The skill level of the administrators managing them

The lifecycle of software and hardware is critical in enterprise environments:
- Software follows release cycles (updates over time)
- Vendors eventually stop supporting older versions (end of maintenance cycle)
- Upgrading servers can be costly and complex, so organizations often prioritize stability and long-term planning
- Hardware may be replaced instead of heavily upgraded due to cost-effectiveness

Virtualization and cloud computing have changed infrastructure management:
- One physical machine can run many virtual machines
- Automation and scripting reduce manual administration
- Cloud providers like AWS, Rackspace, and Microsoft Azure reduce the need for physical upgrades and in-house infrastructure

Software stability levels:
- Beta software: new features, less tested, used for development or early adoption
- Stable software: fully tested and used in production systems
- Open-source projects often release early for community feedback
- Proprietary software tends to remain closed until later stages of development

Backward compatibility:
- Ensures newer systems can still run older software
- Open-source systems often prioritize compatibility and use versioned libraries to maintain support
- Breaking compatibility is avoided unless absolutely necessary

Cost considerations:
- Licensing fees (e.g., Microsoft products) can impact system choice
- Decisions depend on hardware, staffing, expertise, maintenance needs, and future requirements
- Cloud services and virtualization help reduce costs by scaling resources on demand

Interface evolution:
- Early systems used switches, plugboards, and punch cards
- Text-based terminals evolved into modern command line interfaces (CLI)
- Graphical user interfaces (GUI) were developed at
Xerox PARC and popularized by Apple in the 1980s
- Modern operating systems typically support both GUI and CLI, though consumer systems tend to hide CLI complexity from users

## Linux
A Linux distribution (distro) is how most users obtain Linux:
- It bundles the Linux kernel, system utilities, management tools, applications, and update mechanisms.

It also handles system setup tasks like:
- Installing storage systems
- Building/configuring the kernel
- Installing hardware drivers
- Providing package managers for installing/removing/updating software

There are hundreds of Linux distributions, but selection is guided by similar factors as other operating systems:
- Intended role
- Required functions
- Maintenance and support needs

### Role-based flexibility:
Linux can be tailored for many uses:
- Servers (web, application, enterprise systems)
- Desktop systems
- Specialized systems (firewalls, POS systems, electronics design, statistical computing)
- Embedded devices and supercomputers

This makes Linux highly customizable compared to more fixed-purpose operating systems.

Function and support considerations:
- Enterprises may choose distributions with commercial support for reliability.
- Open-source communities provide strong security oversight and rapid bug fixing.

Application compatibility varies:
- Some software supports only specific distributions or versions.
- Widely supported apps like Firefox and LibreOffice work across most distros.

Lifecycle and update models:
- Distributions follow major/minor release cycles.

Two broad categories:
- Enthusiast/rolling or fast-moving distros (e.g., openSUSE Tumbleweed, Fedora, Ubuntu Desktop): frequent updates, newer features, less stability guarantee.

- Enterprise/LTS distros (e.g., Red Hat, SUSE, Canonical LTS): long-term stability, support for ~5–13 years.

<b>Some applications require older OS versions, forcing trade-offs between stability and security.</b>

Stability levels:
- Stable: fully tested and production-ready
- Testing: intermediate stage before stable release
- Unstable/Beta: active development, features may change or break

Community vs enterprise workflows often mirror each other (e.g., Fedora - Red Hat, openSUSE - SLES)

Cost considerations:
Linux itself is <b>usually</b> free, but enterprise support may be paid depending on needs.

Linux supports both GUI and CLI:
- GUI: desktop environments similar to other operating systems, with windows, icons, menus, and login systems.
- CLI: text-based terminal interaction for direct command execution.

How the CLI works:
1. User types commands into a terminal
2. The terminal passes input to a shell
3. The shell interprets and executes commands via the operating system

Output or errors are displayed back in the terminal

CLI systems often include login prompts and optional system messages (MOTD)

Why CLI is important in Linux:
- Efficient for administration and remote management
- Common in servers where GUI would waste resources
- Text-only environments are a continuation of traditional UNIX-style computing

## Linux Distributions
### Red Hat
Started as a Linux distribution introducing the RPM (Red Hat Package Manager).

Evolved into a company focused on enterprise server solutions.

Produced Red Hat Enterprise Linux (RHEL):
Paid, long-term support, stability-focused release cycle.

Designed for enterprise environments prioritizing reliability over frequent updates.

To support users who want newer software, Red Hat sponsors <b>Fedora</b>:

- Community-driven desktop distro
- Faster release cycle with cutting-edge features
- Serves as a testing ground for future RHEL features

Open-source nature led to CentOS:
- Rebuilt RHEL packages for free compatibility
- Largely RHEL-compatible but without official Red Hat support
- Specialized derivatives include Scientific Linux:
- Developed for scientific computing (e.g., Fermilab, CERN/LHC use cases)

---

### SUSE
Originally derived from Slackware.

Developed into a major enterprise Linux distribution similar in scope to Red Hat.

Went through multiple ownership changes but remained active and evolving.

Key variants:
- SUSE Linux Enterprise (SLES): paid, enterprise-grade, includes proprietary components
- openSUSE: free, community-driven version with multiple desktop options

---

### Debian
Community-driven distribution focused on open-source principles and stability.

Introduced the .deb package format and its own package management system.

Supports a wide range of hardware architectures directly.

Forms the base for many derivatives, most notably:
Ubuntu (by Canonical):
- Most widely used Debian-based distribution
- Available in desktop, server, and specialized editions
- Offers LTS (Long-Term Support):
    - 3 years for desktops
    - 5 years for servers

Commercial support available through Canonical
Linux Mint:
- Derived from Ubuntu
- Uses Ubuntu repositories

Some versions include proprietary codecs due to licensing constraints

---

### Android
Built on the Linux kernel but significantly different from traditional Linux distributions.

Uses a different software stack (e.g., Dalvik/ART runtime instead of GNU tools/Xorg).

Generally incompatible with standard desktop Linux software and package systems.

Apps come from ecosystems like Google Play rather than Linux package managers.

Terminal access exists but is limited unless extended (e.g., BusyBox).

Other notable distributions
Raspbian (Raspberry Pi OS):
- Optimized for Raspberry Pi hardware
- Popular in education, embedded systems, robotics, and IoT projects

Linux From Scratch (LFS):
- Educational project guiding users to build a Linux system from source
- Provides deep understanding of OS internals and customization
- Useful for learning or highly specialized systems

---

There are hundreds of Linux distributions, but most share the same core kernel and similar tools.
Differences mainly come from package management, update cycles, purpose, and support models.

---

Linux began as a system for a specific Intel 386 PC setup, but its open-source nature allowed developers to expand hardware support over time, including low-power and specialized processors.

This flexibility led to widespread use in embedded systems—devices designed for specific tasks such as:
- Smartphones
- Smart TVs
- DVRs
- Industrial monitoring and control systems

As hardware evolved, Linux became a foundation for rapidly prototyping devices using affordable components, especially with platforms like the Raspberry Pi, enabling fast development of custom solutions.

Embedded Linux is central to the growth of the Internet of Things (IoT), powering networks of sensors and controllers used in industries like energy, manufacturing, and infrastructure for real-time monitoring and control.

Ongoing integration with AI and machine learning is expected to further improve efficiency, safety, and automation across these systems.
