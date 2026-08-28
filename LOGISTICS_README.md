# Logistics, Furnaces, Sorters, and Stackers

## Programs

- `ArcFurnaceHash.ic10`: loops through fourteen named arc furnaces and calls the furnace routine.
- `ArcFurnaceStackHashWithSorter.ic10`: checks stacker inventory and enables sorting/dispensing for a smaller furnace group.
- `sorter.ic10`: packs ore hashes into sorter filter slots.
- `sorterAutoAssign.ic10`: reads stacker contents, assigns sorter routes by item name, and triggers dispensing.
- `SorterToPrinterOutput.ic10`: routes ingot-class stacks to eight sorters.
- `StackerSingleDispenseSwitchLogic.ic10`: converts a switch action into a one-item sorter dispense command.

## Hash and command conventions

Sorter filter values use the repository convention `(rawHash & 0xffffffff) << 8 | 0x01`. Linked-list lookups and filter slots must compare the packed value, not the raw hash.

The stacker switch program uses ReferenceId values for the stacker, switch, and sorter rather than ordinary `d0`/`d1` wiring. It writes the dispense command to slot 511. The copy under `AutoPrinter/` is the same logic kept with the printer system.

Confirm furnace and device names before using the hash-based programs. Start with one route and one furnace, then expand the configured list.
