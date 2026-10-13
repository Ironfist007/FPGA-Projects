# FPGA Projects (Verilog)

Two digital-design projects implemented in Verilog and deployed on a **Xilinx Spartan-6 FPGA**, developed with **Xilinx ISE**.

| Project | Focus | Key Concepts |
|---|---|---|
| [Traffic Light Controller](./Traffic%20Light%20Controller) | FSM-based sequential design | Finite state machine, timers, UART control |
| [I2C and SPI Protocols](./I2C%20and%20SPI%20Protocols) | Serial communication protocols | Master/slave logic, clock generation, data framing |

---

## Repository Structure

```
FPGA Projects/
├── I2C and SPI Protocols/
│   ├── I2C/
│   │   ├── Master.v          # I2C master controller
│   │   ├── Slave.v           # I2C slave model
│   │   ├── tbmast.v          # Self-checking testbench
│   │   ├── i2c frame.png     # I2C frame diagram
│   │   └── I2C.jpg           # I2C result / capture
│   └── SPI/
│       ├── Master.v          # SPI master (configurable CPOL/CPHA, full-duplex)
│       ├── Slave.v           # SPI slave model
│       ├── Loopback.v        # Loopback configuration (TX -> RX)
│       ├── Master_tb.v       # Master testbench
│       ├── Loopback_tb.v     # Loopback testbench
│       ├── Master.jpg        # Master result / waveform
│       ├── Loopback.jpg      # Loopback result / waveform
│       └── images.png
└── Traffic Light Controller/
    ├── traffic_light.v       # FSM-based T-intersection controller
    ├── test_commands.v       # Testbench driving state transitions / commands
    └── traffic_light.jpg     # Waveform / board result
```

---

## 1. Traffic Light Controller

**FSM-Based Digital System Design on FPGA (Verilog)**

A T-intersection traffic light controller built as a clocked **finite state machine**. It extends earlier combinational-logic work (adders, subtractors, BCD decoder) into sequential design with timer-driven state transitions and phase control logic.

- Clocked FSM with timer-driven state transitions and phase control
- Self-checking testbench that simulates every state transition and timing path in Xilinx ISE
- Synthesized and deployed on a Spartan-6 FPGA, with on-board behavior validated
- Serial control layer: the FSM receives input signals over **UART** from a C++ program, connecting software control to the FPGA hardware end-to-end

**Files:** `traffic_light.v` (design), `test_commands.v` (testbench)

![Traffic light](./Traffic%20Light%20Controller/traffic_light.jpg)

---

## 2. I2C and SPI Protocol Controllers

**Digital Communication Protocol Design on FPGA (Verilog)**

Master-side controllers for the **I2C** and **SPI** protocols, covering clock generation and data framing for synchronous serial peripheral communication.

### I2C
- Start/stop condition generation, ACK/NACK handling, and clock synchronization
- Self-checking testbench (`tbmast.v`) verifying protocol behavior
- Address-phase framing and SCL/SDA transitions validated with a **logic analyzer** against I2C standard-mode timing

![I2C frame](./I2C%20and%20SPI%20Protocols/I2C/i2c%20frame.png)

### SPI
- **SPI Master** with configurable clock polarity/phase (CPOL/CPHA) and full-duplex transfer
- **Loopback** configuration to validate TX/RX integrity without external hardware
- Self-checking testbenches for the master (`Master_tb.v`) and loopback (`Loopback_tb.v`)

![SPI Master](./I2C%20and%20SPI%20Protocols/SPI/Master.jpg)

Both controllers were synthesized and deployed on a Spartan-6 board, and the design was extended to interface with an external peripheral over the FPGA's GPIO pins, demonstrating board-level chip-to-chip communication beyond simulated loopback testing.

---

## Getting Started

### Requirements
- Xilinx ISE Design Suite (ISim for simulation)
- Xilinx Spartan-6 FPGA development board
- USB-UART adapter and a C++ host program (Traffic Light Controller)
- Logic analyzer (optional, for I2C/SPI timing verification)

### Simulation
1. Create a new ISE project and add the design file(s) for the module you want to test.
2. Add the matching testbench (e.g. `Master_tb.v`, `tbmast.v`, `test_commands.v`) as a simulation source.
3. Set the testbench as the top module and run behavioral simulation in ISim.
4. Check the console and waveform for pass/fail output.

### Synthesis and Deployment
1. Set the design module as top.
2. Add a `.ucf` constraints file matching your board's pinout.
3. Run **Synthesize -> Implement -> Generate Programming File**.
4. Program the Spartan-6 board with the generated `.bit` file.

## Skills Demonstrated
- Finite state machine design and timer-driven sequential logic
- Self-checking testbench development
- Serial protocol implementation (UART, I2C, SPI)
- FPGA synthesis, pin constraints, and on-board validation
- Hardware/software integration (C++ to FPGA over UART)
- Signal-level debugging with a logic analyzer

## License
Add your license here (e.g. MIT).
