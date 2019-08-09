# Create Custom Cell for UITableViewCell using a .xib file

## Create an empty View 

Create a new file and select "View" from the "User Interface" section of the file template dialog. 

## Add UI Elements to View 

Since it's an empty view we need to drag in a parent view. Drag a UITableViewCell from the Object Library to the canvas area.

In this example we will drag the following UI elements: 

* 1 UIImageView 
* 2 UILabel(s)

Position the UI elements as per your design spec

## Create a new file that subclass's UITableViewCell 

* Select the UITableViewCell in the .xib file and change its class in the Indentity Inspector to the subclass's name
* Connect the UI Elements from the .xib file over to the UITableViewCell subclass using the Assistant editor

## Update the ViewController

In the viewDidLoad register the Nib as below 

```swift 
tableView.register(UINib(nibName: "NameCell", bundle: nil), forCellReuseIdentifier: "NameCell")
```

Make sure you're downcasting the custom cell in the ```cellForRowAt```

```swift 
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
  guard let cell = tableView.dequeueReusableCell(withIdentifier: "NameCell",
                                                 for: indexPath) as? NameCell else {
    fatalError("Not able to dequeue a NameCell")
  }
  cell.nameLabel.text = names[indexPath.row]
  return cell
}
```
