# EDA (Electronic Design Automation)

### Important Links

* [https://ivlsi.com/synthesis-overview-and-inputs/](https://ivlsi.com/synthesis-overview-and-inputs/)
* [http://smdpc2sd.gov.in/downloads/IEP/IEP%208/24-02-18%20Rejender%20pratap.pdf](http://smdpc2sd.gov.in/downloads/IEP/IEP%208/24-02-18%20Rejender%20pratap.pdf)

### Important concepts

* **VLSI -** Very Large Scale Integration like a microprocessor.
* **Two types of design:**
  * **ASIC** - Application Specific Integration Circuit.
  * **FPGA(Field Programmable Gate Array)** - Multipurpose microchip
* **Two types of implementation:**
  * **Emulation** - On the hardware
  * **Simulation** - On the software

### Steps followed in EDA:

* HDL Source (RTL) using languages like VHDL, Verilog, etc.
* HDL Compiler => No timing info.
* Design Compiler(Optimization + Mapping) => Timing info
* Target Technology.

### Files used in VLSI

* RTL/Verilog(.v) - Info about different components, like combinational and sequential logic. I think it contains the whole design definition.
* .lib(Timing library) - Timing information and also voltage/power info.
* .lef(Physical Library) - Physical info for placement and size.
* .sdc(Standard design constraint) - clock, period, duty cycle, edge times.
