# Linked List Controller

This folder contains a stack-backed linked-list service and the helper programs used by more complex controllers.

- `StackBasedLinkedListCon.ic10`: command processor for add, delete, write, and alternate linked-list operations.
- `DequeHeadTailPrealloc.ic10`: deque host using preallocated storage.
- `DequeHeadTailPreallocMemory.ic10`: add-head/add-tail worker.
- `DequeHeadTailPreallocDelete.ic10`: delete-head/delete-tail worker.
- `FindNodeAtPosition.ic10`: helper that finds a node at a requested list position.
- `StateMachineAirlockControllerLinkedList.ic10`: airlock controller that uses the linked-list service.

The linked-list service uses nodes beginning at slot `32` with stride `4`; command and state data occupy the upper portion of the 512-slot stack. The service command flags are add `$b001000000000`, delete `$b100000000000`, write `$b010000000000`, and alternate `$b000100000000`.

Keep the controller, workers, and shared memory on the layout expected by their matching defines. This is a reusable data-structure subsystem, not a standalone airlock controller.
