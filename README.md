# Tenda AC8 Vulnerability Proof-of-Concepts

This repository contains Proof-of-Concept (PoC) exploits for vulnerabilities discovered in **Tenda AC8** routers.

## Overview

All vulnerabilities and corresponding PoCs in this repository were **discovered by [EleFuzz]** — an adaptive black-box network protocol fuzzer with **fragment-aware** capabilities.

EleFuzz is designed to efficiently discover vulnerabilities in network devices through intelligent mutation, state-aware fuzzing, and fragment-aware test case generation.

## Public Disclosure

These Proof-of-Concepts are **publicly disclosed** to facilitate:
- Security research
- Vulnerability assessment
- Firmware hardening

We believe in responsible disclosure and have followed coordinated disclosure practices with the vendor prior to this public release.

## About EleFuzz

EleFuzz is an **adaptive black-box network protocol fuzzer** that:
- Applies state-aware mutations
- **Performs application-layer message fragmentation guided by differential testing results**
- **Adaptively selects packet fragments as mutation positions during fuzzing**
- Targets proprietary network protocols commonly found in IoT devices

> **Open Source Status**  
> We are actively working with our department to secure approval for open-sourcing EleFuzz.  
> This repository will be updated once EleFuzz becomes publicly available.

## Legal & Responsible Use

These PoCs are provided **for educational and defensive purposes only**.  
Users are solely responsible for complying with applicable laws and regulations.  
Do not use these PoCs against devices you do not own or have explicit permission to test.

## Contact

For questions regarding EleFuzz or these vulnerabilities, please open an issue in this repository.

---

**EleFuzz Research Team — NUDT_EEI**  
*Adaptive, Fragment-Aware Fuzzing for a Safer Internet of Things*
