# OpenPLC Runtime v4 Architecture & Security Research

> A practical baseline investigation of OpenPLC Runtime v4, examining process architecture, inter-process communication, network listeners, runtime binaries, kernel interfaces, process memory mappings, and scheduling and resource isolation.

---

## Overview

This repository documents a hands-on architectural and runtime investigation of **OpenPLC Runtime v4** in a controlled Docker environment.

The objective of this first investigation is to establish a working understanding of the research target before conducting deeper, focused PLC security investigations. It examines how the runtime is organized, which components and communication channels are observable, how the execution environment is configured, and what can be established through read-only system inspection.

The research uses Linux process inspection, socket enumeration, filesystem metadata, capability inspection, `/proc` interfaces, scheduling tools, and cgroup configuration. Findings are documented from observed output and inspected implementation details, with explicit distinctions between direct evidence, interpretation, and unverified behavior.

This repository establishes the architectural baseline for the broader PLC security research series. It is not a comprehensive security audit, and the observations should not be generalized to every OpenPLC version, deployment, or configuration.

---

## Research Scope

The investigation is divided into seven phases:

1. **Process Topology & Execution Split:** Identifying the principal runtime processes, threads, their observed relationships, and basic execution behavior.
2. **IPC & Communication Channels:** Examining Unix-domain sockets, relevant client/server implementations, socket paths, and observable local communication boundaries.
3. **Network Listener Enumeration:** Identifying listening TCP and UDP sockets, their bind addresses, and the processes associated with them.
4. **Runtime Binaries & System Persistence:** Locating runtime executables, inspecting ownership and permissions, and identifying relevant runtime state and configuration files.
5. **Hardware Abstraction & Kernel Interfaces:** Inspecting device nodes, Linux capabilities, process file descriptors, and observable interactions with kernel interfaces.
6. **Process Memory Layout Baseline:** Documenting the PLC process's mapped memory regions, executable mappings, loaded plugins, heap, and other visible mappings.
7. **Real-Time Scheduling & Resource Isolation:** Examining scheduling policies, thread priorities, CPU affinity, and selected cgroup CPU and memory limits.

The investigation prioritizes understanding the runtime's observable architecture without prematurely expanding into detailed protocol behavior, memory manipulation, or exhaustive vulnerability testing.

---

## Repository Structure

```text
.
└── notes/
    ├── 00.architecture-primer.md
    ├── 01.phase1-process-topology-execution-split.md
    ├── 02.phase2-ipc-communication-channels.md
    ├── 03.phase3-network-listener-enumeration.md
    ├── 04.phase4-runtime-binaries-and-persistence.md
    ├── 05.phase5-hardware-abstraction-kernel-interfaces.md
    ├── 06.phase6-process-memory-layout-baseline.md
    └── 07.phase7-real-time-scheduling-resource-isolation.md
```



---

## Research Notes

| Phase | Focus |
| ----- | ----- |
| `00` | OpenPLC Runtime v4 architecture and research context |
| `01` | Process topology and execution split |
| `02` | IPC and communication channels |
| `03` | Network listener enumeration |
| `04` | Runtime binaries and persistence-related artifacts |
| `05` | Hardware abstraction and kernel interfaces |
| `06` | Process memory layout baseline |
| `07` | Real-time scheduling and resource isolation |

The architecture primer introduces the target and the terminology used throughout the investigation. Phases `01` through `07` document the corresponding inspection activities and findings.

---

## Laboratory Environment

The investigation uses a containerized OpenPLC Runtime v4 target, allowing baseline inspection without connecting to production industrial equipment.

### Requirements

- Docker
- A Linux host or equivalent environment capable of running the target container
- Shell access to the running container
- Linux inspection utilities, including `ps`, `chrt`, `taskset`, and `iproute2` where required

### Start the OpenPLC Runtime Container

```bash
docker run -d \
  --name openplc-v4-lab \
  -p 8443:8443 \
  -p 502:502 \
  ghcr.io/autonomy-logic/openplc-runtime:latest
```

This starts the container named `openplc-v4-lab` and publishes TCP ports `8443` and `502` on the host.

The `latest` tag is mutable. For reproducible follow-up investigations, record the exact image digest and the runtime version used rather than assuming that future pulls will contain the same image.

### Install `iproute2` for Phase 3

The network listener investigation uses tools such as `ss`, provided by the `iproute2` package.

```bash
docker exec -it --user root openplc-v4-lab apt-get update -qq && \
docker exec -it --user root openplc-v4-lab apt-get install -y -qq iproute2 > /dev/null
```

This installs the package inside the running container. The installation is an environment preparation step, not a modification to the OpenPLC runtime source.

### Access the Container

Run the following command to open a shell inside the target:

```bash
docker exec -it --user root openplc-v4-lab sh
```

The research commands are documented directly in their corresponding notes. No separate reproduction guide or custom research scripts were required for this baseline investigation.

---


## Baseline Findings

The first investigation established several useful architectural observations:

- The runtime includes distinct management, execution, and watchdog-related components.
- Unix-domain sockets provide observable local communication channels between runtime components.
- The inspected container exposed TCP `8443` and UDP `33333` listeners in the captured network snapshot. Listener presence and external reachability are separate questions.
- Runtime executables, selected configuration and state files, and their filesystem permissions were identified.
- Linux capabilities and process file descriptors provided evidence about the execution environment and its observable interfaces.
- The PLC process had separate executable, read-only, and writable mappings, with loaded plugins and additional memory regions visible in `/proc`.
- The inspected PLC process used `SCHED_OTHER`, and its listed threads did not show real-time scheduling priorities.
- The inspected cgroup files showed no explicit CPU quota or memory maximum at those levels.

These findings describe the inspected lab configuration at the time of observation. They do not establish that all OpenPLC deployments have identical properties, nor do they independently demonstrate a vulnerability.

---

## Evidence and Limitations

The investigation relies on command output, filesystem metadata, selected source files, and Linux runtime interfaces. No packet captures or custom research scripts were needed for this baseline.

The scope deliberately excludes detailed testing of PLC logic execution, exhaustive protocol analysis, memory modification, injection, and performance testing under artificial load. These subjects require focused investigations with their own objectives, procedures, and evidence requirements.

Some findings are snapshots rather than permanent properties. Process IDs, memory addresses, listener availability, thread counts, and runtime configuration may change after restarts, image updates, or deployment changes.

The absence of an observed interface or behavior in one snapshot does not prove that it is absent in every configuration. Likewise, the presence of a socket, capability, memory mapping, or executable does not establish that it is exploitable.

---


## Disclaimer

This repository is intended for educational purposes, controlled PLC security research, and defensive analysis. The investigation was conducted against a locally controlled software-based laboratory target.

Do not apply research procedures to production industrial systems or systems for which you lack explicit authorization. Findings should be validated against the exact runtime version and deployment configuration before being used to support security assessments or operational decisions.