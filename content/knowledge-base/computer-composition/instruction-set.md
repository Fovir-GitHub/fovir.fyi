---
# prettier-ignore
date: 2026-01-04
title: Instruction Set
description: Note if instruction set.
weight: 12
---

## Data Transfer Instructions Overview

<table>
  <tbody>
    <tr>
      <td colspan="2">General Purpose Data Transfer</td>
    </tr>
    <tr>
      <td><code>MOV</code></td>
      <td>Move a byte or a word</td>
    </tr>
    <tr>
      <td><code>PUSH</code></td>
      <td>Push word onto stack</td>
    </tr>
    <tr>
      <td><code>POP</code></td>
      <td>Pop word off stack</td>
    </tr>
    <tr>
      <td><code>XCHG</code></td>
      <td>Exchange bytes or words</td>
    </tr>
    <tr>
      <td><code>XLAT</code></td>
      <td>Table lookup-translation</td>
    </tr>
    <tr>
      <td colspan="2">IN/OUT Instruction</td>
    </tr>
    <tr>
      <td><code>IN</code></td>
      <td>Input</td>
    </tr>
    <tr>
      <td><code>OUT</code></td>
      <td>Output</td>
    </tr>
    <tr>
      <td colspan="2">Address Object Transfer</td>
    </tr>
    <tr>
      <td><code>LEA</code></td>
      <td>Least effective address</td>
    </tr>
    <tr>
      <td><code>LDS</code></td>
      <td>Load pointer using <code>DS</code></td>
    </tr>
    <tr>
      <td><code>LES</code></td>
      <td>Load pointer using <code>ES</code></td>
    </tr>
    <tr>
      <td colspan="2">Flag Transfer</td>
    </tr>
    <tr>
      <td><code>LAHF</code></td>
      <td>Load <code>AH</code> from flags</td>
    </tr>
    <tr>
      <td><code>SAHF</code></td>
      <td>Store <code>AH</code> into flags</td>
    </tr>
    <tr>
      <td><code>PUSHF</code></td>
      <td>Push flags onto stack</td>
    </tr>
    <tr>
      <td><code>POPF</code></td>
      <td>Pop flags off stack</td>
    </tr>
  </tbody>
</table>

## General Purpose Data Transfer

### `MOV`

Copy data from source to destination.

Usage:

```asm
MOV D, S
```

The following situations are not allowed to use `MOV`:

- Memory → Memory
- Immediate → Segment Register
- Segment Register → Segment Register

### `PUSH`

Usage:

```asm
PUSH SRC
```

Process:

1. `SP <- SP - 2`
2. `(SP + 1, SP) <- SRC`

### `POP`

Usage:

```asm
POP DEST
```

Process:

1. `DST <- (SP + 1, SP)`
2. `SP <- SP + 2`

It loads $16$ bits content from `SS:SP` to `DST`.

### `XCHG`

Usage:

```asm
XCHG OPR1, OPR2
```

It exchanges values between two operands.

`XCHG` is not allowed:

- Memory ↔ Memory
- Segment ↔ Registers

### `XLAT`

Usage:

```asm
XLAT
```

Process:

`AL <- DS:[BX + AL]`

## Address Object Transfer

### `LEA`

Load effective address.

Usage:

```asm
LEA REG, SRC
```

Process:

`REG <- SRC`

### `LDS`

Load pointer into `DS`.

Usage:

```asm
LDS REG, SRC
```

Process:

1. `REG <- SRC`
2. `DS <- SRC + 2`

### `LES`

Load pointer into `ES`.

Usage:

```asm
LES REG, SRC
```

Process:

1. `REG <- SRC`
2. `ES <- SRC + 2`

## Flag Transfer

| Instruction | Meaning               | Process                                           |
| ----------- | --------------------- | ------------------------------------------------- |
| `LAHF`      | Load `AH` with flags  | `AH <- (Low byte of PSW)`                         |
| `SAHF`      | Store `AH` into flags | `(Low byte of PSW) <- AH`                         |
| `PUSHF`     | `Push the flags`      | 1. `SP <- SP - 2` <br /> 2. `(SP + 1, SP) <- PSW` |
| `POPF`      | Pop the flags         | 1. `PSW <- (SP + 1, SP)` <br /> 2. `SP <- SP + 2` |

## `IN`/`OUT` Instructions

Usage:

```asm
IN REG, PORT
OUT PORT, REG
```

The `PORT` ranges from $0$ to $\text{FFH}$.

## Arithmetic Instructions

<table>
  <tr colspan="2"><td>Addition</td></tr>
  <tr>
    <td><code>ADD</code></td>
    <td>Add byte or word</td>
  </tr>
  <tr>
    <td><code>ADC</code></td>
    <td>Add byte or word with carry</td>
  </tr>
  <tr>
    <td><code>INC</code></td>
    <td>Increment byte or word by 1</td>
  </tr>
  <tr>
    <td><code>AAA</code></td>
    <td>ASCII adjust for addition</td>
  </tr>
  <tr>
    <td><code>DAA</code></td>
    <td>Decimal adjust for addition</td>
  </tr>
  <tr colspan="2"><td>Subtraction</td></tr>
  <tr>
    <td><code>SUB</code></td>
    <td>Subtract byte or word</td>
  </tr>
  <tr>
    <td><code>SBB</code></td>
    <td>Subtract byte or word with borrow</td>
  </tr>
  <tr>
    <td><code>DEC</code></td>
    <td>Decrement byte or word by 1</td>
  </tr>
  <tr>
    <td><code>CMP</code></td>
    <td>Compare</td>
  </tr>
  <tr>
    <td><code>NEG</code></td>
    <td>Negate byte or word</td>
  </tr>
  <tr>
    <td><code>AAS</code></td>
    <td>ASCII adjust for subtraction</td>
  </tr>
  <tr>
    <td><code>DAS</code></td>
    <td>Decimal adjust for subtraction</td>
  </tr>
  <tr colspan="2"><td>Multiplication</td></tr>
  <tr>
    <td><code>MUL</code></td>
    <td>Multiply byte of word unsigned</td>
  </tr>
  <tr>
    <td><code>IMUL</code></td>
    <td>Integer multiply byte or word</td>
  </tr>
  <tr>
    <td><code>AAM</code></td>
    <td>ASCII adjust for multiply</td>
  </tr>
  <tr colspan="2"><td>Division</td></tr>
  <tr>
    <td><code>DIV</code></td>
    <td>Divide byte or word unsigned</td>
  </tr>
  <tr>
    <td><code>IDIV</code></td>
    <td>Integer divide byte or word</td>
  </tr>
  <tr>
    <td><code>AAD</code></td>
    <td>ASCII adjust for division</td>
  </tr>
  <tr>
    <td><code>CBW</code></td>
    <td>Convert byte to word</td>
  </tr>
  <tr>
    <td><code>CWD</code></td>
    <td>Convert word to double word</td>
  </tr>
</table>

### Addition

| Instructions | Usage           | Process                 |
| ------------ | --------------- | ----------------------- |
| `ADD`        | `ADD DEST, SRC` | `DST <- DST + SRC`      |
| `ADC`        | `ADC DEST, SRC` | `DST <- DST + SRC + CF` |
| `INC`        | `INC DEST`      | `DEST <- (DEST) + 1`    |

### Subtraction

| Instructions | Usage             | Process                 |
| ------------ | ----------------- | ----------------------- |
| `SUB`        | `SUB DST, SRC`    | `DST <- DST - SRC`      |
| `SBB`        | `SBB DST, SRC`    | `DST <- DST - SRC - CF` |
| `DEC`        | `DEC OPR`         | `OPR <- (OPR) - 1`      |
| `NEG`        | `NEG OPR`         | `OPR <- 0 - OPR`        |
| `CMP`        | `CMP OPR1, OPXR2` | `OPR1 - OPR2`           |

### Multiplication

| Instructions | Usage      | Process                                              |
| ------------ | ---------- | ---------------------------------------------------- |
| `MUL`        | `MUL SRC`  | 1. `AX <- AL * SRC` <br /> 2. `(DX, AX) <- AX * SRC` |
| `IMUL`       | `IMUL SRC` | 1. `AX <- AL * SRC` <br /> 2. `(DX, AX) <- AX * SRC` |

### Division

| Instructions | Usage      | Process                                                    |
| ------------ | ---------- | ---------------------------------------------------------- |
| `DIV`        | `DIV SRC`  | 1. `AL <- AX / SRC` <br /> 2. `AH <- AX % SRC`             |
| `IDIV`       | `IDIV SRC` | 1. `AX <- (DX, AX) / SRC` <br /> 2. `DX <- (DX, AX) % SRC` |

#### `CBW`

Usage:

```asm
CBW
```

Process:

`AL -> AX`.

If MSB of `AL` is $1$, then `AH = 255`. Otherwise, `AH = 0`.

#### `CWD`

Usage:

```asm
CWD
```

Process:

`AX -> (DX, AX)`

If MSB of `AX` is $1$, then `DX = 65535`. Otherwise, `DX = 0`.

### Adjusting Instruction of BCD Code

#### `DAA` and `DAS`

These two instructions are used in packed BCD.

- `DAA`: Decimal Adjust after Addition
- `DAS`: Decimal Adjust after Subtraction

If $\text{AL} \; \& \; \text{0FH} > 9$ or `AF = 1`, then $\text{AL} \; \pm= \text{06H}$ and `AF = 1`.

If $\text{AL} \; \& \; \text{F0H} > \text{90H}$ or `CF = 1`, then $\text{AL} \; \pm= \text{60F}$ and `CF = 1`.

#### `AAA` and `AAS`

These two instructions are used in unpacked BCD.

- `AAA`: ASCII Adjust after Addition
- `AAS`: ASCII Adjust after Subtraction

If $\text{AL} \; \& \; \text{0FH} > 9$ or `AF = 1`, then the adjustment happens, and `AF = CF = 1`.

$$
\begin{align*}
  \text{AL} \; &\pm= 6 \\
  \text{AH} \; &\pm= 1 \\
  \text{AL} \; &\&= \text{0FH}
\end{align*}
$$
