<!-- idris
module README

import Data.Fin.Minus
import Data.Vect
import Data.Vect.Dependent
-->

# Dependent `Vect`

Idris 2 library with `Vect` indexed by length with type of elements indexed by its position in the vector.

## Example

Consider you want to have a type-safe diagonal matrix of numbers.
You can use dependent vector for this, e.g.

```idris
DiagMatrix : Nat -> Type -> Type
DiagMatrix n a = DVect n $ \i => Vect (S $ finToNat i) a
```

Then you can create a value of such matrix and compiler would check all the lengths:

```idris
m : DiagMatrix 5 Nat
m = [ [1]
    , [1, 2]
    , [1, 2, 3]
    , [1, 2, 3, 4]
    , [1, 2, 3, 4, 5]
    ]
```

If you need an upside-down triangle, it's easy:

```idris
DiagMatrix' : Nat -> Type -> Type
DiagMatrix' n a = DVect n $ \i => Vect (n - weaken i) a

r : DiagMatrix' 5 Nat
r = [ [1, 2, 3, 4, 5]
    , [1, 2, 3, 4]
    , [1, 2, 3]
    , [1, 2]
    , [1]
    ]
```
