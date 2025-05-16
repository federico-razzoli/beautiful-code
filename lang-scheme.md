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


## Variadic Functions

A variadic function without arguments is like HAL9000 at the end of its life:

```
(define (count-args . args)
  (if (null? args)
      (error "No arguments... Dave, my mind is going...")
      (length args)))
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

