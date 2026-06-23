---
title: "EEE 213: Introduction to Logic"
last_updated: 2026-06-23
---

# EEE 213: Introduction to Logic

A **14-week** course in digital logic, built around **one method** and **one goal**.

The method: every circuit is designed the same way, from a **truth table** to its
**minterms** to a **logic expression** to a **gate circuit**. Sequential circuits use the
same method, with the current state added as extra inputs and the next state as extra outputs.
Because we lock on the **D flip-flop** (where the next state *is* the D input), nothing new is
needed: a sequential circuit is just a combinational truth table with feedback.

The goal: by the last week we assemble those pieces into a **working 4-bit microcontroller**,
load a small program into its ROM, and watch it run.

> **Dr. Şenol Gülgönül**
> Electrical & Electronics Engineering

[🏠 Home](https://senolgulgonul.github.io/logic/)

Every circuit in this course is built and tested in the browser with
[**LogicLab**](https://senolgulgonul.github.io/logiclab/), so there is nothing to install.
Each half of the course is also a hands-on lab: you build one real circuit on a breadboard,
so the theory always meets the hardware. Lab equipment and Arduino resources are gathered in
the [**Lab Annex**](annex-lab-arduino.html) at the end.

This course favours **depth over coverage**. A small number of fundamentals, understood
completely, carries you further than a long list of half-learned topics. Anything not covered
here can be picked up later from the same fundamentals.

---

## The through-line: an MCU is just a logic circuit

Each topic earns its place because it is a part you will need to build the microcontroller:

- The **ALU** is an adder and a subtractor, so we build those.
- The **control unit** is a decoder, some OR gates, and a multiplexer, so we build those.
- The **program counter** is a counter, so we build that.
- The **registers and RAM** are made of D flip-flops, so we build those.
- The **ROM** holds the program, so we build that from a decoder and OR gates first, then see
  how flash memory replaced the wires with transistors.

Assemble them, add a clock, and you have a computer.

---

## How the simulator shows behaviour

In **LogicLab** you place parts, wire output pins to input pins, then press power. A wire glows
when it carries a 1. Switches set inputs, LEDs read outputs, a clock with a single-step button
drives sequential circuits, and a timing panel traces every signal. A LUT4 part lets you drop a
16-entry truth table straight onto the sheet, which is exactly the bridge to FPGAs.

---

## House conventions (matched to the exams)

- One method everywhere: **truth table to minterms to expression to gates**. We use **minterms
  only**; one method is enough.
- **Karnaugh maps with three variables only**, plus **don't-care** conditions. The point is the
  grouping, not the bookkeeping.
- **Huntington postulates** appear only so you can read Shannon's 1937 paper. We do not use them
  to minimise circuits.
- For sequential design: the truth table gains the **current state** as inputs and the **next
  state** as outputs. With a D flip-flop, D is the next state, so there is no excitation table.
- **Active-high** unless an overline marks active-low. This is how you read a real IC datasheet.
- **MSB on the left**; buses are labelled `[n-1:0]`.

---

## 14-Week Plan

### Part A: Combinational logic (Weeks 1-8)

| Week | Topic |
| ---- | ----- |
| [1](weeks/week01-why-logic-history.html)        | **Why logic, and where it came from**: why digital; Aristotle, Boole, Shannon, and Cahit Arf; from logic operators to gates to computers |
| [2](weeks/week02-bits-voltage-adc.html)         | **From the real world to bits**: decimal and binary, what a 0 and a 1 really are (voltage ranges), Schmitt triggers, analog-to-digital conversion |
| [3](weeks/week03-boolean-algebra-gates.html)    | **Boolean algebra and the eight gates**: two-valued algebra, Huntington (just enough for Shannon), theorems and precedence, the eight gates |
| [4](weeks/week04-design-chain-minterms.html)    | **The design chain**: circuit analysis, diagram to expression and back, the V-cycle design guide, minterms to expression to circuit, 7-segment, LogicLab |
| [5](weeks/week05-karnaugh-maps.html)            | **Minimisation with Karnaugh maps**: 3-variable maps only, don't-cares, NAND realisation, XOR and parity, reading datasheets |
| [6](weeks/week06-binary-arithmetic-adder.html)  | **Binary arithmetic and the adder**: half adder, full adder, 4-bit adder, carry propagation, why real ICs are not just cascaded full adders |
| [7](weeks/week07-subtractor-alu.html)           | **Subtraction and a first ALU**: 2's-complement subtraction, 4-bit subtractor, adder vs subtractor as a basic ALU |
| [8](weeks/week08-mcu-combinational-blocks.html) | **The MCU's combinational blocks**: comparator, decoder/demultiplexer (and BCD-to-7-segment), encoder, multiplexer, functions with a MUX and a LUT4 |
| —    | **Study week + MIDTERM** (all of combinational) |

### Part B: Sequential logic and the MCU (Weeks 9-14)

| Week | Topic |
| ---- | ----- |
| [9](weeks/week09-flipflops.html)                   | **The first flip-flop**: the SR latch, the D latch and why latches are a problem, the edge-triggered D flip-flop |
| [10](weeks/week10-sequential-design-truth-table.html) | **Sequential design, one method**: JK and T named for completeness, but we lock on D; design as a truth table of current and next state; the 2-bit counter |
| [11](weeks/week11-counters-program-counter.html)   | **Counters, dividers, and the program counter**: ripple and binary counters, BCD counter, the program counter, frequency division with a D flip-flop |
| [12](weeks/week12-registers-shift-memory-elements.html) | **Registers and memory elements**: the D flip-flop as a 1-bit register, parallel-load and n-bit registers, shift registers, Mealy and Moore as categories |
| [13](weeks/week13-memory-rom-ram.html)             | **Memory**: ROM as a hard-wired decoder plus OR gates, how flash replaced the wires with transistors (EPROM, flash), RAM as a grid of registers |
| [14](weeks/week14-build-the-mcu.html)              | **Build the MCU**: von Neumann vs Harvard; assemble the PC, ROM, control logic, registers A and B, ADD/SUB ALU and RAM; load and run a 6-instruction program |
| —    | **Week 15: Study week** |
| —    | **FINAL** |

---

## Tool and links

- **LogicLab** (browser, no install): <https://senolgulgonul.github.io/logiclab/>
- [**Lab Annex**: lab setup and Arduino resources](annex-lab-arduino.html)
- Companion course, **EEE 303 Digital System Design (Verilog)**: <https://senolgulgonul.github.io/verilog/>
- Reference textbook: M. Morris Mano, *Digital Design*. The course follows its own flow, not the
  book chapter by chapter.

## License

Licensed under **CC BY 4.0**: reuse and adapt freely, including the figures, with attribution.
