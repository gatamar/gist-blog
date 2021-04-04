## UIBezierPath
`⏰ date: 04.04.2021 🪢 tags: #UIKit #linalg`

My mind is blown. I wanted to reverse the math behind this filled curve: 

```
```

Of course this is should be done with `UIBezierPath` primitives, but which funcs to choose?

I've thought of these:
1. Quad curve (it has only 1 control point, but I don't feel this control point).
```
```

2. Fitting some Gaussian curve in the given points, then interpolate more points with (m,sigma) - looks ugly because I'm not sure that there exists a Gaussian curve which fits more-or-less perfectly.   

Then I've seen that `3*3 + 4*4 = 5*5`, so here are 2 arcs of circles with R=5. 
Then I've created a model, which is slightly wrong (unit = `w/(4.33*4)`, not `w/(18)`). I'll fix this if needed.
```
```

The code looks like this:
```
```

This code wants to be rewritten into vectors (left/right/normals), because I need to do this "hats" Top/Bottom/Right/Left, and it would be easy just to rotate vectors.

But while my `exension CGPoint` does have a logic for calculating vector normals, it doesn't know how to work with right/left vectors, so for now I've used `UIBezierPath.apply(_ transform: CGAffineTransform)`.


