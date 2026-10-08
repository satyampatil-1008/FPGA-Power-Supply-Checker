# FPGA-Based Multi-Rail Power Supply Fault Indicator

A hardware-based power supply monitoring system implemented using a **Spartan-6 FPGA (Digilent Atlys board)** and **Verilog HDL**.

The system monitors external **5 V, 9 V, and 12 V DC power supplies** using voltage-divider and comparator circuits. The comparator outputs are converted into safe **3.3 V logic signals** and supplied to the FPGA through the PMOD connector.

The FPGA processes these signals and provides individual **OK indicators** for each power supply along with a common **FAULT indicator**.

---

## 📌 Project Overview

Power supplies are commonly used in electronic systems, and detecting an incorrect or missing supply voltage is important for reliable operation.

This project demonstrates how an FPGA can be used as a digital monitoring unit for multiple DC power rails.

The system checks:

- **5 V supply**
- **9 V supply**
- **12 V supply**

Each supply is first passed through a **voltage divider** to reduce its voltage to a safe sensing level. An **LM339 comparator** then compares this sensing voltage with an adjustable reference voltage.

The comparator generates a digital **OK signal**:

- Logic HIGH → Supply is within the acceptable range
- Logic LOW → Supply is below the set threshold / not OK

These signals are connected to the Spartan-6 FPGA through the PMOD connector.

The FPGA then controls four LEDs:

| LED | Function |
|-----|----------|
| LD0 | 5 V Supply OK |
| LD1 | 9 V Supply OK |
| LD2 | 12 V Supply OK |
| LD3 | Fault Indicator |

---

# 🎯 Objectives

The main objectives of this project are:

1. To monitor multiple external DC power supplies.
2. To safely interface higher external voltages with a 3.3 V FPGA.
3. To use comparators for voltage-level detection.
4. To process comparator outputs using Verilog HDL.
5. To indicate individual supply status using LEDs.
6. To generate a common fault indication when any monitored supply is not OK.
7. To demonstrate practical FPGA interfacing with external analog circuitry.

---

# 🧩 System Block Diagram

```text
                 EXTERNAL POWER SUPPLIES
                         │
          ┌──────────────┼──────────────┐
          │              │              │
         5 V            9 V            12 V
          │              │              │
          ▼              ▼              ▼
    Voltage Divider  Voltage Divider  Voltage Divider
          │              │              │
          ▼              ▼              ▼
       LM339           LM339           LM339
     Comparator       Comparator       Comparator
          │              │              │
          │ 3.3 V        │ 3.3 V        │ 3.3 V
          └──────────────┼──────────────┘
                         │
                         ▼
                Spartan-6 FPGA
                  (Atlys Board)
                         │
             ┌───────────┼───────────┐
             │           │           │
             ▼           ▼           ▼
           LD0         LD1         LD2
          5 V OK       9 V OK      12 V OK
                         │
                         ▼
                      LD3
                  FAULT INDICATOR
