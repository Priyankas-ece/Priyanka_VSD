# Tools Installation (Week 0)

  This document contains installation steps for the basic tools used in Digital VLSI design.

## 1. Yosys (Synthesis Tool)
**Commands:**
- sudo apt-get update
- git clone https://github.com/YosysHQ/yosys.git
- cd yosys
- sudo apt install make (If make is not installed please install it)
- sudo apt-get install build-essential clang bison flex \ libreadline-dev gawk tcl-dev libffi-dev git \ graphviz xdot pkg-config python3 libboost-system-dev \ libboost-python-dev libboost-filesystem-dev zlib1g-dev
- make config-gcc
- make
- sudo make install

**Verification:**
yosys --version

## 2. Icarus Verilog (iverilog)
**Commands:**
- sudo apt-get update
- sudo apt-get install iverilog

**Verification:**
iverilog -V

## 3. GTKWave (Waveform Viewer)
**Commands:**
- sudo apt-get update
- sudo apt install gtkwave

**Verification:**
gtkwave --version

<img width="1920" height="895" alt="Screenshot from 2025-09-20 14-32-49" src="https://github.com/user-attachments/assets/93369ca4-6e9c-405a-b2b6-1cf31897db21" />

<img width="1920" height="888" alt="Screenshot from 2025-09-20 14-33-18" src="https://github.com/user-attachments/assets/5503d050-898b-44bd-aed6-e9210e245730" />
