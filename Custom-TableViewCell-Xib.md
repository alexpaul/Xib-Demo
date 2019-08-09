# Create Custom Cell for UITableViewCell using a .xib file

## Create an empty View 

Create a new file and select "Empty" from the "User Interface" section of the file template dialog. 

## Add UI Elements to View 

Since it's an empty view we need to drag in a parent view. Drag a UITableViewCell from the Object Library to the canvas area.

In this example we will drag the following UI elements: 

* 1 x UIImageView 
* 2 x UILabel(s)

Position the UI elements as per your design specification

## Create a new file that subclass's UITableViewCell 

* Select the UITableViewCell in the .xib file and change its class in the Indentity Inspector to the subclass's name
* Connect the UI Elements from the .xib file over to the UITableViewCell subclass using the Assistant editor

Example file contents 

```swift 
class NameCell: UITableViewCell {
  @IBOutlet weak var profileImage: UIImageView!
  @IBOutlet weak var nameLabel: UILabel!
}
```

## Update the ViewController

In the **viewDidLoad** register the Nib as below 

```swift 
tableView.register(UINib(nibName: "NameCell", bundle: nil), forCellReuseIdentifier: "NameCell")
```

Make sure you're downcasting to the custom cell in the ```cellForRowAt``` method

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

In Objective-C 

```objective-c 
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
  PodcastCell *cell = [tableView dequeueReusableCellWithIdentifier:@"PodcastCell"];
  if (!cell) {
    [tableView registerNib:[UINib nibWithNibName:@"PodcastCell" bundle:nil] forCellReuseIdentifier:@"PodcastCell"];
    cell = [tableView dequeueReusableCellWithIdentifier:@"PodcastCell"];
  }
  Podcast *podcast = self.podcasts[indexPath.row];
  cell.collectionNameLabel.text = podcast.collectionName;
  return cell;
}
```

At this point you should have successfully created and are able to run and see your custom table view cell. 🎉
