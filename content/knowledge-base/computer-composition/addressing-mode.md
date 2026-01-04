---
# prettier-ignore
date: 2026-01-04
title: Addressing Mode
description: Note of addressing mode.
weight: 10
---

## Definition

Addressing mode is the way that the microprocessor identifies the location of the operands or data.

It includes:

- Register direct addressing
- Immediate addressing
- Memory addressing
  - Register indirect addressing
  - Memory direct addressing
  - Displacement addressing
  - Indexed addressing
  - Scaled addressing

## Register Direct Addressing

The operand to be accessed is specified as residing in an internal register.

It involves the use of registers, and memory is not accessed, so it is fast.

Source and destination registers must match in size.

<table>
  <thead>
    <tr>
      <th rowspan="2">Register</th>
      <th colspan="2">Operand Size</th>
    </tr>
    <tr>
      <th>Byte (Reg 8)</th>
      <th>Word (Reg 16)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Accumulator</td>
      <td>AL, AH</td>
      <td>AX</td>
    </tr>
    <tr>
      <td>Base</td>
      <td>BL, BH</td>
      <td>BX</td>
    </tr>
    <tr>
      <td>Count</td>
      <td>CL, CH</td>
      <td>CX</td>
    </tr>
    <tr>
      <td>Data</td>
      <td>DL, DH</td>
      <td>DX</td>
    </tr>
    <tr>
      <td>Stack Pointer</td>
      <td>-</td>
      <td>SP</td>
    </tr>
    <tr>
      <td>Base Pointer</td>
      <td>-</td>
      <td>BP</td>
    </tr>
    <tr>
      <td>Source Index</td>
      <td>-</td>
      <td>SI</td>
    </tr>
    <tr>
      <td>Destination Index</td>
      <td>-</td>
      <td>DI</td>
    </tr>
    <tr>
      <td>Code Segment</td>
      <td>-</td>
      <td>CS</td>
    </tr>
    <tr>
      <td>Data Segment</td>
      <td>-</td>
      <td>DS</td>
    </tr>
    <tr>
      <td>Stack Segment</td>
      <td>-</td>
      <td>SS</td>
    </tr>
    <tr>
      <td>Extra Segment</td>
      <td>-</td>
      <td>ES</td>
    </tr>
  </tbody>
</table>

Examples:

```asm
MOV AX, BX
MOV AL, BL
```

## Immediate Addressing

Immediately following the op code are the data.

These data are supplied by the programmer.

It does not require memory address.

It normally represents constant data.

It can only be used to specify a source operand.

The source operand is a constant.

It is possible to be in all registers except segment and flag registers.

Examples:

```asm
MOV BX, 1234H
MOV CX, 233
ADD AL, 40H
```

## Memory Addressing

The physical address contains:

- **Segment Base Address (SBA):** Identify the starting location of the segment in memory.
- **Effective Address (EA):** Represent the offset of the operand from the beginning of this segment of memory.

### Memory Direct Addressing

Address of the data in memory comes immediately after the instruction operand is a constant.

The address is the offset address.

The offset address is put in a rectangular bracket (`[]`), such as:

```asm
MOV DL, [2400H]
```

And the physical address (PA) is represented as:

```text
PA = Segment Base : Direct Address
OR
PA = segment:offset
```

Segment override prefix (SOP) enables the four segment registers to be referenced.

For example, to move two bytes of `ES:1234H` into `BX`, the following code will work:

```asm
MOV BX, ES:[1234H]
```

### Register Indirect Addressing

The instruction indicates which register contains the needed data.

Indicate a register pair which points to the correct memory address.

The address of the memory location where the operand resides is held by a register.

Examples:

```asm
MOV AL, [BX]
MOV CL, [SI]
```

Only `BX`, `BP`, `SI`, and `DI` can be used.

| Register/Index | Default Segment |
| -------------- | --------------- |
| `BX`           | `DS`            |
| `SI`           | `DS`            |
| `BP`           | `SS`            |
| `DI`           | `SS`            |

### Displacement (Register Relative) Addressing

Example: Move `DS:BX + 10` and `DS:BX + 11` into `CX`:

```asm
MOV CX, [BX] + 10
MOV CX, [BX + 10]
MOV CX, 10[BX]
```

### Indexed Addressing

Examples:

```asm
MOV CL, [BX][DI] ; PA = DS:BX + DI
MOV CH, [BX][SI] ; PA = DS:BX + SI
MOV AH, [BP][DI] ; PA = SS:BP + DI
MOV AL, [BP][SI] ; PA = SS:BP + SI
```

### Scaled Addressing

Examples:

```asm
MOV AX, 4 * [BX]
ADD ECX, [EDI * 4]
ADD ECX, [EBX + EDI * 4 + 1234H]
```

> Scale can only be $1, 2, 4, 8$.

## Offset Registers for Different Segments

| Segment Register | `CS` | `DS`             | `ES`             | `SS`       |
| ---------------- | ---- | ---------------- | ---------------- | ---------- |
| Offset Register  | `IP` | `SI`, `DI`, `BX` | `SI`, `DI`, `BX` | `SP`, `BP` |
