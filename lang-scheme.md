# Beautiful Scheme

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

