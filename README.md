# PLC Security Research

> **Project status: Archived — October 2026**
>
> This repository preserves an earlier research effort focused on OpenPLC v4 runtime architecture and Linux-level implementation details.
>
> The broader Software PLC Security Research project has since been re-scoped around foundational research, practical attack techniques, industrial protocol interactions, and experimentally validated defenses. That work will continue in the separate [`softplc-security-research`](https://github.com/404saint/softplc-security-research) repository.
>
> This repository remains available as a standalone technical case study. Its findings and original scope are preserved for reference.

## About This Investigation

The original investigation examined the architecture and execution environment of the OpenPLC v4 runtime in a Linux-based software PLC deployment.

It established a technical baseline by examining runtime processes, inter-process communication, network listeners, executable components, Linux capabilities, memory mappings, and related runtime behavior.

The investigation focused on understanding the implementation observed in the selected laboratory environment. Its findings should be interpreted within the limits of the tested runtime, configuration, and deployment.

## Investigation

- [`plc-runtime-architecture/`](plc-runtime-architecture/) — OpenPLC v4 runtime architecture and Linux-level implementation analysis.

Refer to the investigation directory for its documentation, methodology, evidence, and findings.

## Scope and Limitations

This work examined a software PLC runtime in a controlled Linux-based laboratory environment.

The investigation does not establish that every observed behavior constitutes a vulnerability. Runtime characteristics, process permissions, capabilities, and deployment choices must be interpreted in context.

A software PLC does not reproduce every characteristic of a physical PLC. Findings from this investigation should not be generalized to other implementations, versions, hardware platforms, or industrial deployments without further validation.

## License

This project is licensed under the Apache License 2.0. See [`LICENSE`](LICENSE) for details.

## Disclaimer

This repository is intended for educational purposes and authorized security research. The findings apply to the implementation and configuration examined and should not be treated as universal conclusions about PLC products or industrial environments.
