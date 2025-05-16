# Beautiful Scheme

## Composition

Scheme doesn't have a composition function, but we can define it:

```
(define (compose f g)
  (lambda (x)
    (f (g x))))
```

This is beautifully, strictly functional: a function takes exactly one argument.

But we can implement it in a less beautiful, more flexible way, accepting a list of arguments:

```
(define (compose f g)
  (lambda args
    (f (apply g args))))
```


## Reversing a List

```
(define (reverse-list lst)
  (define (reverse-helper lst result)
    (if (null? lst)
        result
        (reverse-helper (cdr lst) (cons (car lst) result))))
  (reverse-helper lst '()))
```

`'()` is a syntax sugar for `(quote ())`, which means "this is data, not code".

