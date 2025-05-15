# Beautiful Haskell

## Maybe

`Maybe` is beautifully defined as:

```
data Maybe a = Just a | Nothing
```

Suppose you see Nessie. It's possible that there really is Nessie. But let's face it: it's
unlikely. It's more likely that you had too much booze. However, we can say that what you see is
`Maybe Nessie`. It could be `Just Nessie`, or it could be `Nothing`.


## Nothing

```
safeDivide :: Double -> Double -> Maybe Double
safeDivide _ 0 = Nothing
safeDivide x y = Just (x / y)
```

* First, we define `safeDivide` signature.
* Then, we implement the division by zero. `_` is a blackhole variable for values we don't care about. `Nothing` is a beatiful value to return when the result is undefined.
* Lastly, we implement the division for all other cases.


## We're in a List Comprehension

Given a chess board, find all the possible positions of the two kings.

```
files = ['a'..'h']
ranks = ['1'..'8']

kingPositions = 
    -- output function: a string indicating the kings coordinates
    [ "White King at " ++ [wf, wr] ++ ", Black King at " ++ [bf, br]
    -- nested list comprehensions compute all the combinations as tuples
    -- the Pos variables match each combination (as-pattern)
    | whitePos@(wf, wr) <- [(f, r) | f <- files, r <- ranks]
    , blackPos@(bf, br) <- [(f, r) | f <- files, r <- ranks]
    # make sure that the kings aren't in the same square
    , whitePos /= blackPos
    ]
```


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

```
factorial :: Integer -> Integer
factorial a
  | a < 0     = error "Did you really think I wouldn't notice that a is negative?"
  | otherwise = foldl' (*) 1 [1..a]
```

The unbeautiful thing here is the `foldl'` funciton name, but it is what it is, and it
follows the Haskell naming style. It means "folding from the left", andthe apostroph means
that the function is strict (not lazy).

We could have used `product` instead, but this function is lazy. As a consequence, for
high values of `a` it is subject to stack overflow. If you don't know what this means, ask
Stack Overflow.

