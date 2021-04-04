## UIBezierPath
`⏰ date: 04.04.2021 🪢 tags: #UIKit #linalg`

My mind is blown. I wanted to reverse the math behind this filled curve: 

![image](https://github.com/gatamar/gist_blog/blob/main/resources/uibezierpath_1.png)

Of course this is should be done with `UIBezierPath` primitives, but which funcs to choose?

I've thought of these:
1. Quad curve 
It has only 1 control point, but I don't feel this control point. So the curvature isn't what I've expected.

![image](https://github.com/gatamar/gist_blog/blob/main/resources/uibezierpath_2.png)

2. Fitting some Gaussian curve in the given points, then interpolate more points with (m,sigma) - looks ugly because I'm not sure that there exists a Gaussian curve which fits more-or-less perfectly.   

3. Circle curves. Then I've seen that `3*3 + 4*4 = 5*5`, so here are 2 arcs of circles with R=5. 

![image](https://github.com/gatamar/gist_blog/blob/main/resources/uibezierpath_3.png)

Then I've created a model, which is slightly wrong (unit = `w/(4.33*4)`, not `w/(18)`). I'll fix this if needed.


The code looks like this:
```
private func createHatCurveLayer(p1: CGPoint, p2: CGPoint, type: ConnSlotType) -> CAShapeLayer {
        let path = UIBezierPath()
        
        let len = (p1-p2).length
        let a: CGFloat = 4.33
        let u = len/(a*4)
        let phi: CGFloat = 1.047
        
        let r: CGFloat = 5*u
        
        let po = (p1+p2)/2
        let v_l = CGPoint(x: -2*a*u, y: 0)
        let vy_l = CGPoint(x: -2*a*u, y: -r)
        let vy_r = CGPoint(x: 2*a*u, y: -r)
        
        path.move(to: po+v_l)
        path.addArc(withCenter: po+vy_l, radius: r, startAngle: .pi/2, endAngle: .pi/2-phi, clockwise: false)
        path.addArc(withCenter: po, radius: r, startAngle: -phi - .pi/2, endAngle: -.pi/2, clockwise: true)
        path.addArc(withCenter: po, radius: r, startAngle: -.pi/2, endAngle: -.pi/2+phi, clockwise: true)
        path.addArc(withCenter: po+vy_r, radius: r, startAngle: -.pi-(.pi/2-phi), endAngle: .pi/2, clockwise: false)
        path.close()
```

This code wants to be rewritten into vectors (left/right/normals), because I need to do this "hats" Top/Bottom/Right/Left, and it would be easy just to rotate vectors.

But while my `exension CGPoint` does have a logic for calculating vector normals, it doesn't know how to work with right/left vectors, so for now I've tried to use `UIBezierPath.apply(_ transform: CGAffineTransform)`. But it seems to rotate the layer, so vectors rotation should be easier to control.




