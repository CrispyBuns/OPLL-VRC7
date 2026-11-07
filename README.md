# OPLL-VRC7

## Patch files

- `ym2413.ips` — original YM2413/OPLL patch. Kept unchanged.
- `ym2413-lagrange-english-relocated-experimental.ips` — experimental relocation intended to avoid overwriting data used by the Lagrange Point English translation.

### Experimental Lagrange Point English compatibility patch

This patch redirects the original OPLL hook from the fixed-bank address `$FD80` to `$DF73`, placing the relocated routine and instrument table in an apparently unused area of PRG bank 62 (file offsets `0x7DF83` and `0x7DF96`).

**Important: this patch is unverified.** The relocation assumes PRG bank 62 is mapped at CPU address range `$C000-$DFFF` when the OPLL hook runs. That mapper-state assumption has not yet been confirmed in-game. Do not treat this as a confirmed fix for the English translation hang. Test on a copy of the English-translated ROM with the original OPLL patch applied, and retain an unmodified backup.

The original `ym2413.ips` is not modified by this experimental patch.
