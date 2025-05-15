# Beautiful Haskell

## Maybe

`Maybe` is beautifully defined as:

```
data Maybe a = Just a | Nothing
```

Suppose you see a Klingon. It's possible that there really is a Klingon. But let's face it: it's
unlikely. It's more likely that you had too much booz. However, we can say that what you see is
`Maybe Klingon`. It could be `Just Klingon`, or it could be `Nothing`.
