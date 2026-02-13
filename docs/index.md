# 1-TOPS RV32IMC SoC

RTOS-capable RV32IMC System-on-Chip designed for student silicon tapeout.

---

# 1. Project Overview

## Objective
Design and tapeout a minimal yet robust RV32IMC SoC capable of running FreeRTOS.

## ISA Support
- RV32I
- M Extension
- C Extension
- Zicsr
- Zifencei
- PMP
- Machine + User mode

---

# 2. SoC Architecture

## 2.1 High-Level Block Diagram

(Insert diagram here)

## 2.2 Interconnect

Single-master AXI-Lite architecture.

## 2.3 Clocking

Single clock domain.
PLL integration planned for tapeout.

---

# 3. Memory Map

| Region        | Base Address | Size     | Description |
|--------------|-------------|----------|-------------|
| Boot ROM     | 0x0000_0000 | 64 KB    | Reset vector |
| SRAM         | 0x2000_0000 | 256 KB   | Program/Data |
| CLINT        | 0x0200_0000 | 64 KB    | Timer + SW interrupt |
| PLIC         | 0x0C00_0000 | 4 MB     | External interrupt ctrl |
| UART         | 0x1000_0000 | 4 KB     | Serial |
| SPI          | 0x1001_0000 | 4 KB     | SPI Master |
| I2C          | 0x1002_0000 | 4 KB     | I2C Master |
| DMA (opt.)   | 0x1003_0000 | 4 KB     | Memory transfer engine |

---

# 4. Core Microarchitecture

## 4.1 Pipeline

5-stage in-order pipeline:
- IF
- ID (C decompression)
- EX
- MEM
- WB

## 4.2 M Extension
Iterative multiplier/divider unit.

## 4.3 CSR Block
Implements machine CSRs and interrupt control.

## 4.4 PMP
Region-based physical memory protection.

---

# 5. Interrupt Architecture

## 5.1 Sources
- Machine Timer Interrupt (MTIP)
- Machine Software Interrupt (MSIP)
- External Interrupt (PLIC)

## 5.2 Interrupt Flow

Peripheral → PLIC → Core External Interrupt → CSR handling → RTOS ISR

---

# 6. Memory System

## 6.1 Boot ROM
Stores reset handler and RTOS startup code.

## 6.2 SRAM
Unified instruction and data memory.

No cache (deterministic RTOS behavior).

---

# 7. Peripherals

- UART
- SPI (Master)
- I2C (Master)
- Optional DMA

All peripherals memory-mapped via AXI-Lite.

---

# 8. RTOS Integration

## 8.1 Tick Source
CLINT machine timer.

## 8.2 Context Switching
Triggered by timer interrupt.

## 8.3 Privilege Model
Machine mode kernel.
User mode tasks (optional support).

---

# 9. Verification Strategy

- RTL simulation
- ISA compliance testing
- Directed interrupt testing
- FreeRTOS bring-up validation

---

# 10. Tapeout Plan

## 10.1 Flow
Genus → Innovus → Signoff

## 10.2 Targets
Frequency target: TBD
Area target: TBD
SRAM macro integration planned.

---

# 11. Future Enhancements

- Instruction cache
- Data cache
- Multi-core scaling
- Advanced DMA

