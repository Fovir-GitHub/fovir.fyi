---
# prettier-ignore
date: 2026-01-04
title: Asynchronous Data Transmission
description: Note of asynchronous data transmission.
weight: 11
---

## Definition

- Data are transmitted on the transmit data (TD) line in packets of $7$ or $8$ bits typically.
- Each packet is framed by a start bit $0$ at the beginning and a stop bit $1$ at the end.
- Optionally, a parity bit is inserted before the stop bit, which is used to determine whether the number of bits equal to $1$ included in the data (excluding the stop bit) is even or not.

## Bits in RS-232C

$1$ is called a mark, while $0$ is called a space.

The idle state for an RS-232C line is a $1$ bit (mark).

For example, to transmit an ASCII character `a`, the time consequence is:

```text
TD 0 1000011 01
```

$1000011$ is `a`. The first $0$ is the start bit and the last $1$ is the stop bit.

Since there are $3$ `1` bits in the data, the parity bit is set to $0$.
