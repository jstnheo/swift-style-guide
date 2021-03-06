# BEST PRACTICES #

This is Prolific's Swift best practices document. 

The purpose of these best practices is to help you keep clean and bug free Swift code that is recommended to follow in your daily work.

### Property Observers ###
Cf Apple documentation:

```
Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.
```

You can use 2 types of property observer:

* *willSet* is called just before the property value is stored.
* *didSet* is called right after the property value is stored.

```swift
var intValue: Int = 0 {
	willSet(newIntValue) {
		print("About to set intValue to \(newIntValue)")
  	}
    didSet {
    	print("Set intValue to \(intValue)")
    }
}
```

`didSet` is very useful when working with a data source array so you can automatically refresh the table view or collection view associated with the array.

```
var dataSource: [String] {
	didSet {
		self.tableView.reloadData()
	}
}
```

Be careful to use *didSet* only on an initialized property. A typical example where it is dangerous to use *didSet* is to set an IBOutlet value before the view loaded.

```swift
class myViewController: UIViewController {
	@IBOutlet weak var label: UILabel!
	
	var text: String {
		didSet {
			self.label.text = text
		}
	}
}

let myViewController = UIViewController()
myViewController.text = "Prolific" // Crash because the view controller label has not been initialized yet
```
