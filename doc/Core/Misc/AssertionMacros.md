# Assertion Macros

```cpp
// Full Include Path
#include "Core/Misc/AssertionMacros.h"

// Already included here
#include "CoreMinimal.h"
```

These macros are enabled in Debug and Development builds only.

`checkSlow` and `verifySlow` are enabled in Debug builds only.

```cpp
void AMethod(int n)
{
    // Always evaluated, but only cause an error if enabled.
    verify(n > 0);
    verifyf(n > 0, "n should be greater than zero but %d were given.", n);

    // Only evaluated if enabled
    check(n > 0);
    checkf(n > 0, "n should be greater than zero but %d were given.", n);

    if(n < 0)
    {
        // Checks that this line is never executed
        checkNoEntry();
    }
}

void Init()
{
    // Checks that this line is executed once for the entire lifetime of the program
    checkNoReentry();
}

void DoStuff(int n)

    // Check that this line is not called recursively
    checkNoRecursion();

    if(n > 0)
        DoStuff(n - 1); // Will crash
}

void JustCreated()
{
    // Equivalent of 'throw NotImplementedException()' in C#
    unimplemented();
}

void NonFatalErrorLogs(int n)
{
    // 'ensure' logs the call stack instead of crashing the application.
    // Usually it's used to log that a condition weren't satisfyied, like n <= 0
    // but you still handle the case, like the if-statement below.
    // The call stack is logged once per hit in a session.
    if(ensure(n > 0))
    {
        DoStuff();
    }

    // Like above, but will log always instead of just once.
    ensureAlways(n == 0);

    if(ensureMsgf(n > 0, "This shouldn't happen but n is %d", n))
    {
        return;
    }

    if(ensureAlwaysMsgf(n % 2 == 0, "N is even: %d", n))
    {
        DoStuff();
    }
}
```
