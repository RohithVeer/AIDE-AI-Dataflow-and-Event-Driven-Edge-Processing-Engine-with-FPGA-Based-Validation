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

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/d27c6d2e-76f7-4d01-8140-751ec61e6aff" />



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

