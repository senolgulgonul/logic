---
title: "Annex: Labs and Arduino Resources | EEE 213"
last_updated: 2026-06-23
---

# Annex: Labs and Arduino Resources

[🏠 Home](https://senolgulgonul.github.io/logic/)

The course has **four hands-on labs**. Each idea is done **twice**: once in the LogicLab
simulator, and once on a breadboard with real ICs and an Arduino. Two labs are combinational (the
**half adder**) and two are sequential (the **2-bit counter**).

## Equipment

An **Arduino** (used as a 0 to 5V supply and as a digital instrument that drives inputs and reads
outputs), a **breadboard** and **jumper wires**, **LEDs** with about 330 ohm resistors, and these
logic ICs: **74HC86** (quad 2-input XOR), **74HC08** (quad 2-input AND), and **74HC74** (dual D
flip-flop).

---

## Lab 1: Half adder in LogicLab

**Goal:** build a half adder and confirm its truth table in the simulator.

Place two input switches A and B, an **XOR** gate (its output is the **sum S**) and an **AND**
gate (its output is the **carry C**), and two LEDs. Wire A and B into both gates, power it, and
toggle A and B through 00, 01, 10, 11. Confirm `S = A XOR B` and `C = A AND B`.

[▶ Open the half adder in LogicLab](https://senolgulgonul.github.io/logiclab/?circuit=https%3A%2F%2Fsenolgulgonul.github.io%2Flogic%2Fexamples%2Fw06-half-adder.logiclab.json)

## Lab 2: Half adder with Arduino and logic ICs

**Goal:** build the same half adder on a breadboard and check it against Lab 1.

**Wiring.** Power the ICs from the Arduino's 5V and GND rails. Use one gate of a **74HC86** for
the sum and one gate of a **74HC08** for the carry. Drive A and B from two Arduino output pins,
feed both into the XOR gate (output S) and the AND gate (output C), and read S and C on two
Arduino input pins (or show them on LEDs through 330 ohm resistors).

**Sketch.** This drives all four input combinations and prints the truth table:

```cpp
const int A=2, B=3, S=4, C=5;
void setup(){
  pinMode(A,OUTPUT); pinMode(B,OUTPUT);
  pinMode(S,INPUT);  pinMode(C,INPUT);
  Serial.begin(9600);
  Serial.println("A B | S C");
  for(int a=0;a<2;a++) for(int b=0;b<2;b++){
    digitalWrite(A,a); digitalWrite(B,b); delay(50);
    Serial.print(a); Serial.print(" "); Serial.print(b); Serial.print(" | ");
    Serial.print(digitalRead(S)); Serial.print(" "); Serial.println(digitalRead(C));
  }
}
void loop(){}
```

The printed table should match the one from Lab 1.

---

## Lab 3: 2-bit counter in LogicLab

**Goal:** build a 2-bit synchronous up-counter and watch it count.

Place two **D flip-flops** sharing one clock. Wire `D0 = Q0'` (feed FF0's Q' back to its own D)
and `D1 = Q1 XOR Q0`. Put LEDs on Q0 and Q1. Power it and press the clock's single-step button:
the count should walk 00, 01, 10, 11, 00.

[▶ Open the 2-bit counter in LogicLab](https://senolgulgonul.github.io/logiclab/?circuit=https%3A%2F%2Fsenolgulgonul.github.io%2Flogic%2Fexamples%2Fw10-2bit-counter.logiclab.json)

## Lab 4: 2-bit counter with Arduino and ICs

**Goal:** build the same counter on a breadboard and check it against Lab 3.

**Wiring.** Power a **74HC74** (two D flip-flops) from 5V and GND, and tie both clock inputs to a
common clock line driven by an Arduino pin. For FF0, connect its Q' output back to its own D so it
toggles every clock. For FF1, drive D1 from a **74HC86** XOR of Q1 and Q0. Read Q0 and Q1 on
Arduino input pins, or show them on LEDs.

**Sketch.** This generates the clock and prints the count each cycle:

```cpp
const int CLK=2, Q0=4, Q1=5;
void setup(){
  pinMode(CLK,OUTPUT); pinMode(Q0,INPUT); pinMode(Q1,INPUT);
  Serial.begin(9600);
}
void loop(){
  digitalWrite(CLK,HIGH); delay(250);
  digitalWrite(CLK,LOW);  delay(250);
  int count = (digitalRead(Q1)<<1) | digitalRead(Q0);
  Serial.println(count);   // expect 0,1,2,3,0,1,2,3,...
}
```

---

## Using the Arduino as a bench tool

You do not program the Arduino as the subject of the course; you use it to power and probe the
logic you built. Two patterns cover both labs:

- Drive a logic input with 5V or 0V: `digitalWrite(pin, HIGH)` or `digitalWrite(pin, LOW)`.
- Read the state of a logic output: `int s = digitalRead(pin)`.

The **Serial Plotter** is useful for watching several signals change over time.

## Beyond the labs: the MCU cross-check

To show the final MCU is not a toy, the same six-instruction program it runs can be written as an
Arduino sketch (`LDA, LDB, ADD, SUB, STS, NOP` as a tiny interpreter). Running it both ways gives
the same result, which is the point: the gate-level machine and a real MCU do the same thing.
