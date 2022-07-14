### Debugging techniques
1. Add `.border`/`.background` modifiers to see the actual layout of the view.
2. See the layout tree actual type (not hidden by `var body: some View` opaque type):
``` swift
extension View {
	func debug() -> Self {
		print(Mirror(reflecting: self).subjectType)
		return self
	} 
}

var body: some View { 
	VStack { /*... */ }.debug()
}
```

### Mysterious bugs 
1. `Accessing StateObject's object without being installed on a View. This will create a new instance each time.`

![image](https://github.com/gatamar/gist_blog/blob/main/resources/swiftui-issue-1.png)
