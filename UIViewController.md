#### view.layoutIfNeeded()
- Lays out the subviews immediately, if layout updates are pending.
#### view.setNeedsLayout()
- Invalidates the current layout of the receiver and triggers a layout update during the next update cycle.


#### View Dismiss
[source](https://stackoverflow.com/questions/28760541/programmatically-go-back-to-previous-viewcontroller-in-swift)

```Swift
    //to previous view
    navigationController?.popViewController(animated: true)
    //to root view
    navigationController?.popToRootViewController(animated: true)
```
