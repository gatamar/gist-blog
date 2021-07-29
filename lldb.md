### Symbolic breakpoints

Symbolic breakpoint for ObjC selector:
```
-[UIView addSubview:]
```

Action for this breakpoint: 
```
po $arg3
```
where `arg3` is the first parameter of a function. More details: 
https://stackoverflow.com/a/15513459/2567725

`UIScrollView` usage:
```
-[UIScrollView setContentOffset:]
po $arg1
```
