# Beautiful Haskell

## Maybe

`Maybe` is beautifully defined as:

```
data Maybe a = Just a | Nothing
```

Suppose you see Nessie. It's possible that there really is Nessie. But let's face it: it's
unlikely. It's more likely that you had too much booze. However, we can say that what you see is
`Maybe Nessie`. It could be `Just Nessie`, or it could be `Nothing`.


## Fibonacci

```
fibonacci :: Int -> Integer
fibonacci a
  | a < 0     = error "Did you really think I wouldn't notice that a is negative?"
  | a == 0    = 0
  | a == 1    = 1
  | otherwise = fibonacci (a-1) + fibonacci (a-2)
```

This is my favourite, but apparently the Haskell Glasgow Compiler doesn't optimise this code.
Dasnae matter, buddy: the next version is smashing, too.

```
fibonacci :: Int -> Integer
fibonacci a
  | a < 0     = error "Did you really think I wouldn't notice that a is negative?"
  | otherwise = fibs !! a
  where
    fibs = 0 : 1 : zipWith (+) fibs (tail fibs)
```

Instead of a loop, we use recursion passing `(tail fibs)`. Which is an infinite list passed to a function,
yes. But it's ok because Haskell, unlike the Forth Bridges builders, is lazy.


## Factorial



