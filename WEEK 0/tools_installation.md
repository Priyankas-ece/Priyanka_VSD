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
