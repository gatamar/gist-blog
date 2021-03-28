### Minimise usage of state variables
```
date: 28.03.2021
tags: #swift
```

Recently I've had such code:

```
var someLayer: CAShapeLayer?
func updateSomeStateParam(){
  someLayer?.removeFromSuperLayer()
  someLayer = nil
  
  if someCond { return }
  
  someLayer = CAShapeLayer()
  someLayer!.strokeColor = UIColor.red.cgColor
  someLayer!.fillColor = UIColor.blue.cgColor
  someLayer!.frame = self.layer.bounds
  someLayer!.path = UIBezierPath().path
  self.layer.addSublayer(someLayer!)
}
```

There was 14 occurences of `someLayer` in a file, and 7 of them in a func `updateSomeStateParam`.
That's ugly. That's hard to read and navigate. 
I've refactored it like that: 

```
var someLayer: CAShapeLayer?
func updateSomeStateParam(){
  someLayer?.removeFromSuperLayer()
  someLayer = nil
  
  if someCond { return }
  let newLayer = CAShapeLayer()
  newLayer.strokeColor = UIColor.red.cgColor
  newLayer.fillColor = UIColor.blue.cgColor
  newLayer.frame = self.layer.bounds
  newLayer.path = UIBezierPath().path
  someLayer = newLayer
  self.layer.addSublayer(someLayer!)
}
```

Now it looks better. It reminds me smth about the stateless functional programming, but I know almost nothing of it.
Probably a func which creates a new layer could be `static` and know nothing of a current class' state.
I guess it would be easier to test.
