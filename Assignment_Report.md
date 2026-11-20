# Assignment 4 – Modelling Real-World Data with Structures and Unions

**Student:** Alan Godwin J  
**Register Number:** 1921260244  
**Repository:** `CSA02-1911260250-Assignment4`  
**GitHub link:** [ADD AFTER CREATING THE REPOSITORY]

## Submission note
The task folders contain C implementations and captured outputs. The report below provides concise design and complexity notes. Measurements shown by the programs are sample local executions, not claims of large-scale benchmarking. Add your own terminal screenshots and timing tables on your Mac before submission.

## Task 1 – Data design review
Parallel arrays can become misaligned when a record is inserted, deleted or sorted. A phone number is text, may contain a leading zero and needs room for the terminating null byte; `char[16]` is safer for common international formats. Blood pressure must be represented by two integers, not one float. A date should be a nested `{day, month, year}` structure. Check capacity before insertion and avoid global mutable state. An array of structures keeps each patient's fields together and makes sorting records straightforward.

## Task 2 – Nested parcel structures
Entities: Parcel, Address, Date. Address and Date are nested in Parcel. `p[2].to.pincode` accesses the third parcel's receiver PIN; with `struct parcel *q`, use `(q+2)->to.pincode`. Selection sort is O(n²) and swaps complete structures.

## Task 3 – Tagged union
Only one sensor value is valid at a time, so a tagged union stores a tag plus the largest union member. The union size is determined by its largest member and alignment; the enclosing structure may include padding. Always inspect the tag before reading a union member. Reading a different member is not a valid way to convert the stored value.

## Task 4 – Structure pointers
Passing a structure by value modifies only a local copy. Pass `struct account *` to update the caller's balance and use `->`. Use a const pointer when a function only reads a structure. Passing by value is reasonable for small immutable structures.

## Task 5 – Storage classes
An automatic local variable is recreated on each call; a static local variable retains its value for the program lifetime but has block scope. An extern declaration refers to a global object defined elsewhere. A register hint requests fast storage but does not guarantee it; its address cannot be taken. For independent counters, caller-owned integers passed by pointer provide explicit state and avoid hidden shared state.

## Task 6 – Canteen design challenge
Use an Item structure with common fields and a tagged union for packaged expiry date, cooked preparation time or combo component IDs. Sales must validate quantity and stock before decrementing stock. Revenue is quantity times unit price. Expiry warnings compare date structures and should use a well-defined date arithmetic routine. Sort a separate summary by revenue. Array lookup is O(n); linked-list insertion at the head is O(1), while search/removal by key is O(n), with pointer overhead per node.
