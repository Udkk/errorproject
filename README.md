Here's a detailed explanation of the three error handling techniques in Solidity:

1. Revert

The revert statement is used to undo all changes made by the current transaction and revert to the previous state. When a revert statement is executed, the following happens:

All changes made to the contract's state are undone.
The transaction is rolled back, and the contract's state is restored to its previous state.
The transaction is marked as failed, and any gas consumed by the transaction is refunded.
An error message can be provided to explain why the transaction was reverted.


2. Require

The require statement is used to validate conditions and revert if they are not met. When a require statement is executed, the following happens:

The condition is evaluated, and if it is false, the transaction is reverted.
The transaction is rolled back, and the contract's state is restored to its previous state.
The transaction is marked as failed, and any gas consumed by the transaction is refunded.
An error message can be provided to explain why the transaction was reverted.


3. Assert

The assert statement is used to validate conditions and throw an exception if they are not met. When an assert statement is executed, the following happens:

The condition is evaluated, and if it is false, an exception is thrown.
The transaction is terminated, and the contract's state is not changed.
The transaction is marked as failed, and any gas consumed by the transaction is refunded.
An error message can be provided to explain why the transaction failed.






require to validate that the caller is the teacher and the grade is within a valid range
assert to validate that the student's grade is not already set
revert to undo the transaction if the grade is too low
