# OPLL-VRC7 — Lagrange Point

This repository contains the OPLL/VRC7 audio patch work and Lagrange Point patch experiments.

## Confirmed working English + OPLL setup

The working order has been tested by the repository maintainer:

1. Start with a clean Japanese **Lagrange Point** ROM.
2. Remove the 16-byte iNES header (the 16 bytes at the beginning of the file).
3. Apply the original OPLL/VRC7 patch, `ym2413.ips`, to the headerless ROM.
4. Apply the English translation patch **after** the OPLL patch.

The resulting ROM boots, plays OPLL audio, loads/creates saves, and opens the in-game RPG menu correctly in the reported tests.

**Patch order matters.** Do not apply the English translation before `ym2413.ips` for this working setup. The OPLL patch must be applied to the headerless ROM; applying it with the iNES header still present shifts its file offsets by 16 bytes.

Keep a backup of the clean Japanese ROM. Do not distribute copyrighted ROM data; use legally obtained ROM files and patch files.

## Patch files

- `ym2413.ips` — original YM2413/OPLL patch. Kept unchanged.
- `lagrange.ips` — Lagrange Point IPS patch artifact already present in this repository.
- `Lagrange Point (Japan) (patched) (1) (patched).bps` — BPS patch artifact already present in this repository.
- `hex.txt` — hexadecimal dump retained for analysis/reference.
- `ym2413-lagrange-english-relocated-experimental.ips` — experimental relocation patch; superseded for the confirmed working setup.
- `ym2413-lagrange-bank-safe-experimental.ips` — experimental bank-switching patch; not required for the confirmed working setup.

## Experimental relocation patches

The relocation patches are separate experiments. They are **not required** for the confirmed working English + OPLL setup above. Do not apply them as additional stages when reproducing the working result.

