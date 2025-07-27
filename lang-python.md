# Beautiful Python

## Swapping Variables

We can use list unpacking:

```
a, b = b, a
```


## List Rotating (In-Place)

Right-rotating a list in-place:

```
lst.insert(0, lst.pop())
```


## List Rotating (Copy)

Right-rotating a list:

```
lst_rotated = [lst[-1]] + lst[:-1]
```

Left-rotating a list:

```
lst_rotated = lst[1:] + [lst[0]]
```

## Reversing Lists

```
lst = lst(a[::-1])
```

This equally works with strings and tuples.

