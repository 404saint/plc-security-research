# PLC Security Research

![License](https://img.shields.io/badge/License-Apache--2.0-F5A623?style=flat-square&labelColor=242629)
![Focus](https://img.shields.io/badge/Focus-PLC_Security-F5A623?style=flat-square&labelColor=242629)
![Domain](https://img.shields.io/badge/Domain-ICS_%2F_OT-F5A623?style=flat-square&labelColor=242629)
![Lab](https://img.shields.io/badge/Lab-Software--Only-F5A623?style=flat-square&labelColor=242629)
![Method](https://img.shields.io/badge/Method-Evidence--Driven-F5A623?style=flat-square&labelColor=242629)

A hands-on research series investigating Programmable Logic Controller (PLC) security through runtime analysis, engineering workflows, control logic integrity, vulnerability research, and defensive testing using free, software-only labs.

## Overview

This repository documents an ongoing research series examining the security of software-defined PLCs and their surrounding environments. The research focuses on how controllers execute programs, expose management interfaces, accept engineering changes, maintain runtime state, and interact with simulated industrial processes. Each investigation combines practical experimentation with source-code analysis, traffic inspection, reproducible testing, and technical documentation where applicable. The objective is to develop a deeper understanding of PLC security through evidence-driven research using freely available software.

## Research Areas

| Area                                                                                                                    | Focus                                                                         | Status       |    
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------- | :----------: |
| 01. [`plc-runtime-architecture/`](https://github.com/404saint/plc-security-research/tree/main/plc-runtime-architecture) | Target baseline, execution model, and potential attack surfaces               | 🟢 Complete  |
| 02. `plc-program-compromise/`                                                                                           | Unauthorized logic modification, program replacement, and deployment abuse    | ⚪ Candidate |
| 03. `plc-runtime-manipulation/`                                                                                         | Runtime state manipulation and control execution interference                 | ⚪ Candidate |
| 04. `plc-management-compromise/`                                                                                        | Management interfaces, APIs, authentication, and access control               | ⚪ Candidate |
| 05. `plc-process-deception/`                                                                                            | PLC state, HMI visibility, and simulated process discrepancies                | ⚪ Candidate |
| 06. `plc-component-attacks/`                                                                                            | Runtime plugins, libraries, and internal communication                        | ⚪ Candidate |
| 07. `plc-platform-isolation/`                                                                                           | Privilege abuse, filesystem access, and isolation boundaries                  | ⚪ Candidate |
| 08. `plc-persistence-recovery/`                                                                                         | Persistence, update integrity, rollback, and recovery weaknesses              | ⚪ Candidate |
| 09. `plc-availability-attacks/`                                                                                         | Execution disruption, resource exhaustion, and failure behavior               | ⚪ Candidate |
| 10. `plc-detection-defense/`                                                                                            | Attack detection, defensive controls, and mitigation validation               | ⚪ Candidate |

> Research areas are investigative directions, not a fixed sequence or a commitment to produce one investigation per area. New attack hypotheses may emerge as experiments progress.

## Research Methodology

Each investigation follows a question-driven approach adapted to the selected target and research objective.

1. Understand the target
2. Establish a baseline
3. Form a hypothesis
4. Design the experiment
5. Collect evidence
6. Analyze the results
7. Evaluate defenses
8. Document the findings

> Note: Not every investigation will identify a vulnerability. Reproducible negative results and validated security assumptions are also valuable research outcomes.

## Laboratory Environment

The research is designed around a free, software-only environment.

Depending on the investigation, the laboratory may use:

* Open-source/Beremiz PLC runtimes and engineering environments
* Linux virtual machines and containers
* Simulated industrial processes and HMI software
* Python, C, Go, and shell-based research tools
* Wireshark, tshark, and other packet-analysis utilities
* Debuggers, source-code analysis, and automated testing tools

Individual experiments will document their actual requirements, dependencies, configuration, and limitations.

> Note: No physical PLC hardware or paid software is required by the series design. The capabilities of each software-defined target will be evaluated individually, and conclusions will remain within the limits of the environment tested.

## Repository Structure

Each research area is organized as a self-contained investigation containing the documentation, scripts, and evidence relevant to its objectives.

A typical investigation may include:

* `README.md` — research overview, scope, and reproduction instructions
* `notes/` — technical analysis and investigation records
* `scripts/` — experiment harnesses and supporting utilities
* `evidence/` — logs, test results, and other collected artifacts
* `screenshots/` — selected visual evidence

Additional directories, such as `pcaps/`, may be included when the investigation requires them.

> Note: The structure may evolve as the research progresses.

## Intended Audience

* ICS/OT security researchers
* Industrial cybersecurity engineers
* Product security and vulnerability researchers
* Penetration testers working with industrial systems
* Students and practitioners studying PLC internals and industrial control security

> Note: The repository emphasizes practical investigation and reproducible evidence rather than introductory PLC programming tutorials.

## Scope and Limitations

This project primarily investigates software-defined PLC environments and their supporting software.

A simulated controller does not reproduce every characteristic of a physical PLC, including vendor-specific firmware, hardware protections, certified safety mechanisms, and device-specific behavior. Findings will identify the tested implementation and version wherever possible.

Firmware analysis may be considered where it directly supports a research question, but physical hardware exploitation and hardware-dependent testing are outside the core software-only scope.

All experiments are intended for isolated, controlled laboratory environments. Testing against systems without authorization is outside the scope of this project.

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

## Disclaimer

This repository is intended for educational purposes and authorized security research. The techniques and tools documented here should only be used in environments where testing is explicitly permitted.

The findings apply to the implementations and configurations examined. They should not be generalized to all PLC products or industrial environments without further validation.
