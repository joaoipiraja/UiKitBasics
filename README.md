# UiKitBasics
UiKit Basics: Guding Resources for "Now For Real Challenge" - Apple Developer Academy IFCE 

## Core Data

### 1 - Create a Data Model File

### 2 - On App Delegate

#### Core Data Saving Support 

```swift
 func saveContext () {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {

                let nserror = error as NSError
                fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
            }
        }
    }
   
```

```swift
func applicationWillTerminate(_ application: UIApplication) {

        self.saveContext()
    }
```

#### Core Data stack
```swift
 lazy var persistentContainer: NSPersistentContainer = {

        let container = NSPersistentContainer(name: "DataModel")
        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {

                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
        return container
    }()
```

## Alert

```swift
  var textField = UITextField()
        let alert = UIAlertController(title: "Add New Todoey Item", message: "", preferredStyle: .alert)
        let action = UIAlertAction(title: "Add Item", style: .default) { (action) in
        
        }
     alert.addTextField { (alertTextField) in
            alertTextField.placeholder = "Create new Item"
            textField = alertTextField
        }
        alert.addAction(action)
        present(alert, animated: true,completion: nil)       
```

## TableView

### Configure

#### TableView Delegate

```swift
override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        //print(itemArray[indexPath.row])
                
        if tableView.getAccessoryType(indexPath: indexPath) == .checkmark{
            tableView.setAccessoryType(indexPath: indexPath, accessoryType: .none)
        }else{
            tableView.setAccessoryType(indexPath: indexPath, accessoryType: .checkmark)
        }
        
        tableView.deselectRow(at: indexPath, animated: true)
        
    }
```

#### TableView DataSource Methods

```swift
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 3 //create 3 cells
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell  = tableView.dequeueReusableCell(withIdentifier: "Identifier", for: indexPath)
        cell.textLabel?.text = "titulo"
        return cell
    }
```
