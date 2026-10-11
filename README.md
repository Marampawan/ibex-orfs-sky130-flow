# Automated RTL-to-GDSII Physical Implementation of RISC-V Cores (SkyWater 130nm)

This repository contains physical design implementation collaterals, timing constraint configurations, sign-off reports, and layout graphics for two 32-bit RISC-V processors (**Ibex RV32IMC** and **riscv32i**) implemented with **OpenROAD Flow Scripts (ORFS)** on the **SkyWater 130nm (`sky130hd`)** open-source PDK.

---

## 1. PPA Sign-off & Comparative Analysis

The table below summarizes Power, Performance, and Area (PPA) sign-off metrics. Target clock frequencies were pushed to characterize critical path limits, accompanied by closed zero-slack sign-off numbers.

| Metric / Parameter | Ibex Core (RV32IMC) | RISCV-32I Core |
| :--- | :--- | :--- |
| **Technology PDK** | SkyWater 130nm (`sky130hd`) | SkyWater 130nm (`sky130hd`) |
| **EDA Toolchain** | Yosys, OpenROAD, TritonRoute | Yosys, OpenROAD, TritonRoute |
| **Design Area** | **172,822 μm²** | **77,599 μm²** |
| **Core Utilization** | **67%** | **56%** |
| **Sequential Cells (DFFs)** | **1,939** | **1,056** |
| **Clock Tree Buffers / Inverters** | **350** | **214** |
| **Timing Repair Buffers** | **3,174** | **981** |
| **Pushed Target Frequency ($F_{\text{target}}$)** | 117.78 MHz ($T_{\text{clk}} = 8.49\text{ ns}$) | 158.86 MHz ($T_{\text{clk}} = 6.29\text{ ns}$) |
| **WNS at Target Frequency** | -0.55 ns | -0.47 ns |
| **TNS at Target Frequency** | -321.74 ns | -35.47 ns |
| **Timing-Closed Frequency ($F_{\max}$ @ 0 WNS)** | **~110.6 MHz** ($T_{\text{clk}} = 9.04\text{ ns}$) | **~147.9 MHz** ($T_{\text{clk}} = 6.76\text{ ns}$) |
| **Worst Hold Slack (WHS)** | **0.00 ns** (Met) | **0.00 ns** (Met) |
| **Total Power Dissipation** | 65.5 mW | 24.7 mW |
| **Routing DRC Violations** | **0** | **0** |
| **DRV Violations (Max Slew / Cap)** | **0** | **0** |

---

## 2. Physical Layout Views

### Ibex Core Layout (Sky130HD)
![Ibex Layout](images/ibex_layout.png)

### RISCV-32I Core Layout (Sky130HD)
![RISCV-32I Layout](images/riscv32i_layout.png)

---

## 3. Physical Flow Stages Completed
1. **Logic Synthesis:** Synthesized using Yosys targeting standard cell library `sky130_fd_sc_hd`.
2. **Floorplanning & PDN:** Core grid and IO pin placement, power ring and strap generation.
3. **Placement:** Global placement, timing-driven optimization, and legal detailed placement.
4. **Clock Tree Synthesis (CTS):** Balanced clock buffer tree synthesis with low skew.
5. **Detailed Routing:** TritonRoute achieving 0 DRC violations.
6. **Sign-off STA & DRC:** Setup/hold timing validation, transition/capacitance rule checks, and geometric verification.

---

## 4. Repository Structure & Reproducibility

```text
├── configs/
│   ├── ibex/          # Floorplan & SDC timing constraints for Ibex
│   └── riscv32i/      # Floorplan & SDC timing constraints for RISCV-32I
├── images/            # Layout visualization captures
├── reports/           # Detailed routing DRC and final sign-off reports
└── README.md
make DESIGN_CONFIG=./designs/sky130hd/ibex/config.mk
make DESIGN_CONFIG=./designs/sky130hd/riscv32i/config.mk
