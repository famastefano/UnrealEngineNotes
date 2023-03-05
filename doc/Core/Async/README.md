# Async Operations

```cpp
#include "Core/Async/Async.h"
```

The `Async` function allows an easy way to run a function asynchronously.

It allows you to:
1. Choose where the function will be executed
2. Which function to execute
3. Optionally, a callback that will be called when the task has been completed

---

```cpp
#include "Core/Async/ParallelFor.h"
```

Uses the Task Graph Library to easily run a for in parallel.

The work will be done in a callback `void(int32)` that recieves the iteration index.

```cpp
#include "Core/Async/TaskGraphInterfaces.h"
```

The Task Graph Library used by the Engine to dispatch tasks on threads.
