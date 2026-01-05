---
# prettier-ignore
date: 2026-01-05
title: Instruction Format
description: Note of instruction format.
weight: 13
---

## Composition of Instruction

- **Operation Code (Op code):** Tell CPU what to do.
- **Operands:** Tell CPU the content of doing action, including source operand and destination operand.

## Types of Instruction

- **Three-address Instruction** and **Two-address Instruction**: General-purpose register machine.
- **One-address Instruction:** Accumulator-based machine.
- **Zero-address Instruction:** Stack machine.

## Instruction Format

```text
| 7 6 | 5 4 3 | 2 1 0 |
  MOD    REG     R/M
```

### MOD

<table>
  <thead>
    <tr>
      <td>MOD</td>
      <td>Meaning</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>00</code></td>
      <td>
        <table>
          <thead>
            <tr>
              <td><code>R/M</code></td>
              <td>Operation</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>100</code></td>
              <td>SIB</td>
            </tr>
            <tr>
              <td><code>110</code></td>
              <td>Memory direct addressing mode (Displacement only addressing mode) (16-bit displacement)</td>
            </tr>
            <tr>
              <td><code>101</code></td>
              <td>Memory direct addressing mode (Displacement only addressing mode) (32-bit displacement)</td>
            </tr>
            <tr>
              <td>Other</td>
              <td>Register indirect addressing mode with no displacement</td>
            </tr>
          </tbody>
        </table>
      </td>
    </tr>
    <tr>
      <td><code>01</code></td>
      <td>One-byte signed displacement follows addressing bytes</td>
    </tr>
    <tr>
      <td><code>10</code></td>
      <td>Four-byte signed displacement follows addressing bytes</td>
    </tr>
    <tr>
      <td><code>11</code></td>
      <td>Register addressing mode</td>
    </tr>
  </tbody>
</table>

### REG

| REG Value | Register (8-bits) | Register (16-bits) | Register (32-bits) |
| --------- | ----------------- | ------------------ | ------------------ |
| `000`     | `AL`              | `AX`               | `EAX`              |
| `001`     | `CL`              | `CX`               | `ECX`              |
| `010`     | `DL`              | `DX`               | `EDX`              |
| `011`     | `BL`              | `BX`               | `EBX`              |
| `100`     | `AH`              | `SP`               | `ESP`              |
| `101`     | `CH`              | `BP`               | `EBP`              |
| `110`     | `DH`              | `SI`               | `ESI`              |
| `111`     | `BH`              | `DI`               | `EDI`              |
