---
title: Registers
date: 2025-10-17
description: Introduction of registers.
weight: 3
---

## Definition

Register is a quickly accessible location available to a computer's CPU, which usually consists of a small amount of fast storage.

## Size of Registers

- 8-bit register
- 32-bit register
- 64-bit register

## Types of Registers

### User-accessible Registers

It can be read or written by machine instructions.

It has the following types:

- **Data Registers:** A special data register, known as the accumulator, is used implicitly for many operations.
- **Address Registers**
- **General-purpose Registers (GPRs):** It can store both data and addresses.
- **Status Register (Flag Register / Condition Code Register (CCR) / FLAGS Register / Program Status Word (PSW) Register):** It is a collection of status flag bits for a processor.
- **Floating-point Registers (FPRs):** They store floating point numbers in many architectures.
- **Constant Registers:** They hold read-only values such as zero, one, or $\pi$.
- **Vector Registers:** They hold data for vector processing done by **Single Instruction, Multiple Data (SIMD)** instructions.
- **Special-purpose Registers (SPRs):**
  - They hold program states.
  - Include the program counter (instruction pointer), and the status register.
  - Program counter and status register might be combined in a program status word (PSW) register.
- **Model-specific Registers (Machine-specific Registers):** They store data and settings related to the processor itself.

### Internal Registers

It can not be accessible by instructions, and it is used internally for processor operations.

An **instruction register** holds the instruction currently being executed.

There are some registers related to fetching information from RAM:

- **Memory Buffer Register (MBR)**
- **Memory Data Register (MDR)**
- **Memory Address Register (MAR)**

## Register 8086

<table>
  <thead>
    <tr>
      <th colspan="17">
        The 8086 Register
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="17">Main Register (Data Registers)</td>
    </tr>
    <tr>
      <td colspan="5">AH</td>
      <td colspan="5">AL</td>
      <td colspan="7">AX (Primary Accumulator)</td>
    </tr>
    <tr>
      <td colspan="5">BH</td>
      <td colspan="5">BL</td>
      <td colspan="7">BX (Base Accumulator)</td>
    </tr>
    <tr>
      <td colspan="5">CH</td>
      <td colspan="5">CL</td>
      <td colspan="7">CX (Counter Accumulator)</td>
    </tr>
    <tr>
      <td colspan="5">DH</td>
      <td colspan="5">DL</td>
      <td colspan="7">DX (Accumulator, Other Function)</td>
    </tr>
    <tr>
      <td colspan="17">Index or Pointer Register</td>
    </tr>
    <tr>
      <td colspan="5">SI</td>
      <td colspan="12">Source Index</td>
    </tr>
    <tr>
      <td colspan="5">DI</td>
      <td colspan="12">Destination Index</td>
    </tr>
    <tr>
      <td colspan="5">BP</td>
      <td colspan="12">Base Pointer</td>
    </tr>
    <tr>
      <td colspan="5">SP</td>
      <td colspan="12">Stack Pointer</td>
    </tr>
    <tr>
      <td colspan="17">Flag Register</td>
    </tr>
    <tr>
      <td>15</td>
      <td>14</td>
      <td>13</td>
      <td>12</td>
      <td>11</td>
      <td>10</td>
      <td>9</td>
      <td>8</td>
      <td>7</td>
      <td>6</td>
      <td>5</td>
      <td>4</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>Bit Position</td>
    </tr>
    <tr>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>O</td>
      <td>D</td>
      <td>I</td>
      <td>T</td>
      <td>S</td>
      <td>Z</td>
      <td>-</td>
      <td>A</td>
      <td>-</td>
      <td>P</td>
      <td>-</td>
      <td>C</td>
      <td>Flags (CAPSZO + IDT)</td>
    </tr>
    <tr>
      <td colspan="17">Segment Registers</td>
    </tr>
    <tr>
      <td colspan="8">CS</td>
      <td colspan="9">Code Segment</td>
    </tr>
    <tr>
      <td colspan="8">DS</td>
      <td colspan="9">Data Segment</td>
    </tr>
    <tr>
      <td colspan="8">SS</td>
      <td colspan="9">Stack Segment</td>
    </tr>
    <tr>
      <td colspan="8">ES</td>
      <td colspan="9">Extra Segment</td>
    </tr>
    <tr>
      <td colspan="17">Instruction Pointer</td>
    </tr>
    <tr>
      <td colspan="8">IP</td>
      <td colspan="9">Instruction Pointer</td>
    </tr>
  </tbody>
</table>

## FLAGS Register

It contains the current state of the processor.

### Sizes

- **FLAGS Register:** 16 bits
- **EFLAGS Register:** 32 bits
- **RFLAGS Register:** 64 bits

### Types of FLAGS

#### Status Flags

It determines the kind of the result of arithmetic execution.

##### The Carry Flag (CF)

It determines whether there is a carry from the MSB on addition or there is a borrow into the MSB on subtraction.

##### The Parity Flag (PF)

It determines whether the result is even.

##### The Auxiliary Flag (AF)

It determines whether there is a carry from bit 3 on addition or a borrow into the bit 3 on subtraction.

##### The Zero Flag (ZF)

It determines whether the result is zero.

##### The Sign Flag (SF)

It determines whether the MSB is $1$.

##### The Overflow Flag (OF)

It determines whether signed overflow occurred.

##### Determine CF and OF

Suppose both numbers have 8 bits.

On the addition:

For example:

$1111 \; 1111 + 0000 \; 0001 = 1 \; 0000 \; 0000$ will cause a carry on the most left bit, then the `CF` will be turned on, but the `OF` will not be turned on.

The change of `OF` will happen only when both numbers have the same signs, which is potential to be signed overflowed.

For example:

$1000 \; 0000 + 1000 \; 0000 = 1 \; 0000 \; 0000$. The sign changed to $0$, meaning the overflow occurs, so the `OF` will be turned on as well as `CF`.

On the subtraction:

There are two operands: minuend and subtrahend.

The subtrahend can be transformed to its two's complement at first, and then to perform the addition.

When performing the addition, we can get the `CF` and `OF`. And the correct `CF` and `AF` are the inverse of addition's while the correct `OF` is the same as addition's.

#### Control Flags

Control flags are used to enable or disable certain operations of microprocessor, which includes:

- Directional Flag (D)
- Interrupt Flag (I)
- Trap Flag (T)

##### Directional Flag

It is used in string instructions to determine the direction of accessing string data.

If it is $1$, then it means accessing string data from higher memory location towards lower one. Otherwise, it will access string data from lower memory location to higher one.

##### Interrupt Flag

It is used to tell the microprocessor whether to interrupt when accessing to this flag.

If this is set to $1$, the microprocessor will interrupt at this bit, Otherwise, the microprocessor will ignore it.

#### System Flags

They are useful for operating system designer, security management, and for supporting multimedia applications.
