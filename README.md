# OPLL-VRC7

## Patch files

- `ym2413.ips` — original YM2413/OPLL patch. Kept unchanged.
- `ym2413-lagrange-english-relocated-experimental.ips` — first relocation experiment. Superseded by the bank-switch-aware experiment below; do not use it for the current test.
- `ym2413-lagrange-bank-safe-experimental.ips` — second-stage experimental patch for testing on a Japanese Lagrange Point ROM that already has the original `ym2413.ips` applied.

### Bank-switch-aware relocation experiment

Apply this IPS **on top of a Japanese ROM already patched with the original `ym2413.ips`**. It is an add-on test patch, not a standalone OPLL patch and not the English-compatible combined ROM.

The patch redirects the OPLL hook at file offset `0x00A6E` to code at CPU address `$DF73` in VRC7 PRG bank 62. The relocated routine:

1. Reads the current `$C000-$DFFF` bank marker from `$DFFF` and saves it on the stack.
2. Maps PRG bank 62 into `$C000-$DFFF` by writing `$3E` to the VRC7 PRG Select 2 register at `$9000`.
3. Runs the OPLL write routine and reads its instrument table from `$DF95`.
4. Restores the previous bank marker to `$9000`, restores the routine's accumulator value, and jumps back to the original continuation at `$8AE2`.

The game's existing bank-switch helper reads `$DFFF` to preserve the currently mapped C000 bank and restores it through `$9000`; bank 62's marker byte is `$3E`. The chosen code/table area at file offset `0x7DF83` is unused fill in both the Japanese and English ROMs.

**Status: experimental and untested in an emulator.** This patch is intended first to test the bank-switching wrapper on the known-good Japanese + original OPLL setup. It does not prove English-translation compatibility. Do not apply it to an English ROM for the next test.

The original `ym2413.ips` and the first relocation experiment remain unchanged.
