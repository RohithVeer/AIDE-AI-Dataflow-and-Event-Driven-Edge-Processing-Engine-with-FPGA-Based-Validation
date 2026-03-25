# AIDE: AI Dataflow & Event Engine  
### FPGA-Assisted Edge Processing System on Caravel SoC

---

##  Overview

**AIDE (AI Dataflow & Event Engine)** is a lightweight hardware accelerator designed for efficient edge AI systems.

It combines:
- Dataflow-aware processing
- Memory access optimization
- Event-driven computation

The system is implemented on the **Caravel SoC (SKY130)** and validated using the **Vicharak Shrike FPGA board** for real-time data generation.

---

##  System Architecture

### High-Level Flow


FPGA (Shrike) → Streaming Data → Caravel ASIC → Event Detection → Interrupt → CPU


---

### Architecture Diagram


FPGA (Shrike)
|
v
Data Generator + Pattern Injection
|
v
UART / SPI Interface
|
v
Caravel SoC
|
v
+-----------------------------------------+
| Memory Optimizer |
| Dataflow Controller |
| Event Detection Engine |
+-----------------------------------------+
|
v
Interrupt / Output


---

##  System Components

###  FPGA (Vicharak Shrike)

Acts as a **real-time data source and validation platform**.

**Functions:**
- Sensor data generation (temperature, vibration, signals)
- Pattern injection (normal / anomaly scenarios)
- UART/SPI streaming interface
- Real-time hardware testbench

---

### 🔹 ASIC (Caravel User Project)

Implements the **AIDE hardware engine** inside the Caravel user project area.

---

##  Core RTL Modules

### 1. Memory Access Optimizer
- Address generation 
- Prefetch buffer (FIFO) 
- Access scheduling FSM 

### 2. Dataflow Controller
- Data routing 
- Pipeline control 
- Priority arbitration 

### 3. Event Detection Engine
- Threshold detection 
- Peak detection 
- Window-based feature extraction 
- Event-triggered interrupt 

### 4. Wishbone Interface
- Memory-mapped registers 
- CPU configuration and control 

---

##  Operation Flow

1. FPGA generates streaming input data 
2. Data is transmitted via UART/SPI 
3. ASIC receives and buffers data 
4. Memory optimizer schedules access 
5. Dataflow controller routes data 
6. Event engine processes and detects patterns 
7. Interrupt is generated for CPU 

---

##  Caravel Design Constraints (ChipFoundry)

- Caravel SoC harness (RISC-V based) 
- User Project Area (~10 mm²) 
- Wishbone bus interface (mandatory) 
- SKY130 process technology 
- OpenLane RTL-to-GDSII flow 
- RTL + Gate-Level Simulation (GLS) required 

---

##  Tools & Methodology

### RTL Design
- Verilog HDL 

### Simulation
- Icarus Verilog 
- Verilator 
- GTKWave 

### Physical Design
- OpenLane 
- Yosys 
- OpenROAD 
- Magic VLSI 

### FPGA Development
- Vicharak Shrike toolchain 
- UART/SPI communication 

---

##  Repository Structure


AIDE/
├── rtl/ # ASIC RTL modules
├── fpga/ # FPGA data generator and interface
├── sim/ # Testbenches
├── docs/ # Documentation and diagrams
├── openlane/ # Physical design configuration
└── README.md


---

##  Applications

- Industrial monitoring systems 
- Edge AI preprocessing 
- Smart sensor nodes 
- Real-time anomaly detection 

---

##  Key Contributions

- Lightweight AI dataflow architecture 
- Memory-aware processing engine 
- Event-driven computation model 
- FPGA + ASIC co-design 
- Full silicon-to-system workflow 

---

##  Feasibility

- Fits within Caravel user project area (~10 mm²) 
- Compatible with SKY130 standard cells 
- Optimized for low resource usage 
- Suitable for limited compute environments 
- FPGA implementation uses minimal LUTs 

---

##  Development Plan

| Phase | Task |
|------|------|
| Phase 1 | RTL design |
| Phase 2 | Simulation and verification |
| Phase 3 | FPGA prototype implementation |
| Phase 4 | OpenLane synthesis and PnR |
| Phase 5 | Final validation |

---

##  Conclusion

AIDE demonstrates a complete **silicon-to-system workflow**, combining:

- Custom RTL accelerator design
- Caravel SoC integration 
- FPGA-based real-time validation 

---

##  Status

Proposal submitted for ChipFoundry Reference Application Design Contest.
ChipFoundry: https://chipfoundry.io/
=======
<div align="center">

<img src="https://umsousercontent.com/lib_lnlnuhLgkYnZdkSC/hj0vk05j0kemus1i.png" alt="ChipFoundry Logo" height="140" />

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Inter&size=44&duration=3000&pause=600&color=4C6EF5&center=true&vCenter=true&width=1100&lines=Caravel+User+Project+Template;OpenLane+%2B+ChipFoundry+Flow;Verification+and+Shuttle-Ready)](https://git.io/typing-svg)

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![ChipFoundry Marketplace](https://img.shields.io/badge/ChipFoundry-Marketplace-6E40C9.svg)](https://platform.chipfoundry.io/marketplace)

</div>

## Table of Contents
- [Overview](#overview)
- [Documentation & Resources](#documentation--resources)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Starting Your Project](#starting-your-project)
- [Development Flow](#development-flow)
- [GPIO Configuration](#gpio-configuration)
- [Local Precheck](#local-precheck)
- [Checklist for Shuttle Submission](#checklist-for-shuttle-submission)

## Overview
This repository contains a user project designed for integration into the **Caravel chip user space**. Use it as a template for integrating custom RTL with Caravel's system-on-chip (SoC) utilities, including:

* **IO Pads:** Configurable general-purpose input/output.
* **Logic Analyzer Probes:** 128 signals for non-intrusive hardware debugging.
* **Wishbone Port:** A 32-bit standard bus interface for communication between the RISC-V management core and your custom hardware.

---

## Documentation & Resources
For detailed hardware specifications and register maps, refer to the following official documents:

* **[Caravel Datasheet](https://github.com/chipfoundry/caravel/blob/main/docs/caravel_datasheet_2.pdf)**: Detailed electrical and physical specifications of the Caravel harness.
* **[Caravel Technical Reference Manual (TRM)](https://github.com/chipfoundry/caravel/blob/main/docs/caravel_datasheet_2_register_TRM_r2.pdf)**: Complete register maps and programming guides for the management SoC.
* **[ChipFoundry Marketplace](https://platform.chipfoundry.io/marketplace)**: Access additional IP blocks, EDA tools, and shuttle services.

---

## Prerequisites
Ensure your environment meets the following requirements:

1. **Docker** [Linux](https://docs.docker.com/desktop/setup/install/linux/ubuntu/) | [Windows](https://docs.docker.com/desktop/setup/install/windows-install/) | [Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
2. **Python 3.8+** with `pip`.
3. **Git**: For repository management.

---

## Project Structure
A successful Caravel project requires a specific directory layout for the automated tools to function:

| Directory | Description |
| :--- | :--- |
| `openlane/` | Configuration files for hardening macros and the wrapper. |
| `verilog/rtl/` | Source Verilog code for the project. |
| `verilog/gl/` | Gate-level netlists (generated after hardening). |
| `verilog/dv/` | Design Verification (cocotb and Verilog testbenches). |
| `gds/` | Final GDSII binary files for fabrication. |
| `lef/` | Library Exchange Format files for the macros. |

---

## Starting Your Project

### 1. Repository Setup
Create a new repository based on the `caravel_user_project` template and clone it to your local machine:

```bash
git clone <your-github-repo-URL>
pip install chipfoundry-cli
cd <project_name>
```

### 2. Project Initialization

> [!IMPORTANT]
> Run this first! Initialize your project configuration:

```bash
cf init
```

This creates `.cf/project.json` with project metadata. **This must be run before any other commands** (`cf setup`, `cf gpio-config`, `cf harden`, `cf precheck`, `cf verify`).

### 3. Environment Setup
Install the ChipFoundry CLI tool and set up the local environment (PDKs, OpenLane, and Caravel lite):

```bash
cf setup
```

The `cf setup` command installs:

- Caravel Lite: The Caravel SoC template.
- Management Core: RISC-V management area required for simulation.
- OpenLane: The RTL-to-GDS hardening flow.
- PDK: Skywater 130nm process design kit.
- Timing Scripts: For Static Timing Analysis (STA).

---

## Development Flow

### Hardening the Design
Hardening is the process of synthesizing your RTL and performing Place & Route (P&R) to create a GDSII layout.

#### Macro Hardening
Create a subdirectory for each custom macro under `openlane/` containing your `config.tcl`.

```bash
cf harden --list         # List detected configurations
cf harden <macro_name>   # Harden a specific macro
```

#### Integration
Instantiate your module(s) in `verilog/rtl/user_project_wrapper.v`.

Update `openlane/user_project_wrapper/config.json` environment variables (`VERILOG_FILES_BLACKBOX`, `EXTRA_LEFS`, `EXTRA_GDS_FILES`) to point to your new macros.

#### Wrapper Hardening
Finalize the top-level user project:

```bash
cf harden user_project_wrapper
```

### Verification

#### 1. Simulation
We use cocotb for functional verification. Ensure your file lists are updated in `verilog/includes/`.

**Configure GPIO settings first (required before verification):**

```bash
cf gpio-config
```

This interactive command will:
- Configure all GPIO pins interactively
- Automatically update `verilog/rtl/user_defines.v`
- Automatically run `gen_gpio_defaults.py` to generate GPIO defaults for simulation

GPIO configuration is required before running any verification tests.

Run RTL Simulation:

```bash
cf verify <test_name>
```

Run Gate-Level (GL) Simulation:

```bash
cf verify <test_name> --sim gl
```

Run all tests:

```bash
cf verify --all
```

#### 2. Static Timing Analysis (STA)
Verify that your design meets timing constraints using OpenSTA:

```bash
make extract-parasitics
make create-spef-mapping
make caravel-sta
```

> [!NOTE]
> Run `make setup-timing-scripts` if you need to update the STA environment.

---

## GPIO Configuration
Configure the power-on default configuration for each GPIO using the interactive CLI tool.

**Use the GPIO configuration command:**
```bash
cf gpio-config
```

This command will:
- Present an interactive form for configuring GPIO pins 5-37 (GPIO 0-4 are fixed system pins)
- Show available GPIO modes with descriptions
- Allow selection by number, partial key, or full mode name
- Save configuration to `.cf/project.json` (as hex values)
- Automatically update `verilog/rtl/user_defines.v` with the new configuration
- Automatically run `gen_gpio_defaults.py` to generate GPIO defaults for simulation (if Caravel is installed)

**GPIO Pin Information:**
- GPIO[0] to GPIO[4]: Preset system pins (do not change).
- GPIO[5] to GPIO[37]: User-configurable pins.

**Available GPIO Modes:**
- Management modes: `mgmt_input_nopull`, `mgmt_input_pulldown`, `mgmt_input_pullup`, `mgmt_output`, `mgmt_bidirectional`, `mgmt_analog`
- User modes: `user_input_nopull`, `user_input_pulldown`, `user_input_pullup`, `user_output`, `user_bidirectional`, `user_output_monitored`, `user_analog`

> [!NOTE]
> GPIO configuration is required before running `cf precheck` or `cf verify`. Invalid modes cannot be saved - all GPIOs must have valid configurations.

---

## Local Precheck
Before submitting your design for fabrication, run the local precheck to ensure it complies with all shuttle requirements:

> [!IMPORTANT]
> GPIO configuration is required before running precheck. Make sure you've run `cf gpio-config` first.

```bash
cf precheck
```

You can also run specific checks or disable LVS:

```bash
cf precheck --disable-lvs                    # Skip LVS check
cf precheck --checks license --checks makefile  # Run specific checks only
```
---

## Checklist for Shuttle Submission
- [ ] Top-level macro is named user_project_wrapper.
- [ ] Full Chip Simulation passes for both RTL and GL.
- [ ] Hardened Macros are LVS and DRC clean.
- [ ] user_project_wrapper matches the required pin order/template.
- [ ] Design passes the local cf precheck.
- [ ] Documentation (this README) is updated with project-specific details.
