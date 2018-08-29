---
layout: tutorial_pages
part: 12
title: Reloading and Animating your Table View
permalink: /calculator-part-12/
---

In Part 11, we found out our Table View doesn't actually work yet. We have the delegate set up and written out, but appears when the buttons are pressed.

We have to tell the Table View when it needs to reload, by calling the `reloadData()` function on it. Problem is, we haven't set up an `@IBOutlet` for our TableView yet. We can't tell the Table View to do anything until we have an IBOutlet reference to it.

Go ahead and connect an outlet named `tableView`. I trust that you know how to do that with your eyes closed by now (maybe keep your eyes open).

### Reloading and Animating
Telling the tableView to reload is only one line of code, but animating is a little bit more involved than that. This marks a great time to add a new function, so we don't have to copy and paste this code all over the place.

We'll start off with a simple little function. This can be anywhere in the `ViewController.swift`, but it would make the most sense to be near the other Table View code.

```swift
func reloadTable() {
    tableView.reloadData()
}
```

That's all we need to have the Table View reload, but if we add a little more we can get a nice animation to go with it:

```swift
func reloadTable() {
    tableView.reloadData()
    
    let lastIndex = calculations.previousExpressions.count - 1
    let indexPath = IndexPath(item: lastIndex, section: 0)
    if lastIndex > 0 {
        tableView.scrollToRow(at: indexPath, at: .bottom, animated: true)
    }
}
```

### Calling the function

Now we have our `reloadTable()` function, but we'd still have the same problem as before since we don't call this function anywhere.

We'd want to reload the table any time the user presses Enter or Clear, so we just have to add a `reloadTable()` to the end of those respective functions.

They should look like this now:

```swift
@IBAction func equalsButtonPressed(_ sender: AnyObject) {
    calculations.clearInputAndSave(true)
    resultLabel.text = calculations.resultNumber.roundedString
    reloadTable()
}

@IBAction func clearButtonPressed(_ sender: UIButton) {
    calculations.clearInputAndSave(false)
    resultLabel.text = calculations.resultNumber.roundedString
    reloadTable()
}
```

### Testing
Run the app in the simulator again. If you did everything right, your table view should be working great.

<p align="center"> <img src="../images/calculator/P12/screenshot1.gif" align="center"> </p>

### Recap
We added a new function `reloadTable()` to handle reloading and animating the Table View.

You've implemented a fully-functional Calculator app. Congradulations!

### Next Time
That's it, we're all done! 

You learned about Interface Builder, Autolayout Constraints, Delegates, and Table Views. These skills are extremely important in the iOS world and are the building blocks you need to make any app.

If you have feedback on the tutorial, you can email us at iosgatech@gmail.com.
