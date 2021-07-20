So it seems I will learn it soon. 
I've tried raywenderlich tutorial, it's good but not enough - I don't understand the high-level logic.
Need to find a better source.

Today after a while of procrastinating I've "just coded" few more screens in my pet project. There's a modal `Settings` screen, and it has a table view which links (`pushVC`) to much more screens.
Almost every of those screens has a `Close` button at right-top. It looks like this:
```
public override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
    self.navigationController?.navigationBar.topItem?.title = "About the app"
    let button = UIBarButtonItem(title: "Close", style: .done, target: self, action: #selector(onCloseButtonPressed))
    self.navigationItem.rightBarButtonItem = button
}
```
There're such problems: 
1. The logic of "close button" is duplicated in each screen
2. This "close button", or "title" etc is shown too late - in `viewDidAppear`. But if I put it in `viewDidLoad`/`viewDidLayoutSubviews`, it's also bad - when pushed VC is dismissed, we need to update the NavigationController's title anyway.

So I guess `1`&`2` should be done by Coordinator. 

