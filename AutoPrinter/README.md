# AutoPrinter System

This folder contains the queue, request, routing, and printer-control pieces for an automated printer and silo network.

## Programs

- `QueueRequestReceiver.ic10`: receives requests from multiple senders and maps items to routes.
- `PrinterStackerStckExecution.ic10`: reads printer recipe requirements and stacker quantities, then requests missing materials.
- `PrinterImportGate.ic10`: watches autolathe import counts and clears a printer waiting latch when material arrives.
- `SiloSplitterRouter.ic10`: routes packed paths through a splitter graph.
- `SiloSplitterRouterBlankLayout.ic10`: one-time setup program that writes the seven-branch splitter graph.
- `DequeControllerSingleWorker.ic10` + `DequeSingleWorker.ic10`: host and worker for a single-worker deque.
- `DequeHeadTailPrealloc.ic10` + `DequeHeadTailPreallocMemory.ic10` + `DequeHeadTailPreallocDelete.ic10`: host, add worker, and delete worker for the preallocated multi-worker deque.
- `StackerSingleDispenseSwitchLogic.ic10`: copy of the root logistics helper.

## Shared deque layout

The deque buffer is normally slots `32`-`479`. Status is at `504`, result at `509`, argument at `510`, and command at `511`. Status values are `1` success, `-1` empty, `-2` full, and `-3` bad command. Single-worker commands are `1` add head, `2` add tail, `3` delete head, and `4` delete tail.

Load the blank layout only for initial router setup. Keep the host and its matching workers on the same memory device and do not change slot defines independently.
