# Flutter 

Notes taken by me during learning Flutter...

## Why Flutter?
- Most frameworks use native frameworks. but flutter uses its own rendering engine to draw the widgets on the canvas which is our screen

To work with column 
- main axis will be vertical 
- cross axis will be horizontal
inverse for the row


---

## Text decoration

To give text some sexy decoration use this code snippet.

```dart 
Text(
    "This is login page",
    style: TextStyle(
        fontSize: 25, color: Colors.orange, fontWeight: FontWeight.bold),
    textScaler: TextScaler.linear(1.2), // Used to scale the text
),
```


---

## Image

for using an image to our code follow th following format

```dart 

    Image.asset(
      'asset/images/completion.png',
      fit: BoxFit.cover,
    ),

```

---

## Google Fonts

To use google fonts in your project 

```bash
flutter pub add google_fonts
```

then


```dart 
 theme: ThemeData(
          fontFamily: GoogleFonts.tenaliRamakrishna().fontFamily,
          primaryTextTheme: GoogleFonts.tenaliRamakrishnaTextTheme()),

```

---

## Sized box

To add vertical spacing in any two of the widgets use following widget instead of padding or margin 

```dart
SizedBox(
  height: 20,
),
```

We can use ```SizedBox``` as text lable by using following syntax

```dart 
SizedBox(
  height: 20,
  child: Text("Hello"),
),
```

---

## TextField
To play with some of the text input widgets here is one of the widget which let's you play with the inputs

```dart
 TextFormField(
  obscureText: true, //Used to hide the text similar to passwordField
  decoration: InputDecoration(
      hintText: "Enter Password", // Text which will be shown as a hint after clicking on the textField
      labelText: "Password", // Text which is the actual label of our textField
      hintStyle: TextStyle(fontSize: 20) // Some font customization stuff
      ),
)
```

---

## Button

To use buttons in the project use following snippet 

```dart 
ElevatedButton( //Type of the button
  onPressed: () {   // What will happen after pressing on that button
    print("Hello Bharat"); 
  },
  child: Text("Submit"), // Highlighted text which will appear on the actual button
)

```
---

## Git

Here are some useful git commands I might have foregotten 

```bash
git init    # To initialize an empty local repository
git add .   # To add all the files to git 
git branch bname    # To careate new local branch
git switch bname    # To switch between branches 
git branch  # To enlist all the branches available and also to check on which branch we are currently working 
git branch -d bname # To delete the branch
git commit -m "This is required message" # Commit our changes with an required message
git branch -M main # Maybe add all the changes to main branch
git remote add origin {Remote git repo url} # Add all your changes to the remote repository
git push -u origin main # Commit and create the pull request to an remote repo on main branch
git push --set-upstream origin bname    #That specific branch will be stored as main branch
```
---

## Scroll View

If the app screen is overflowing in either way then it is essential to fit all our widgets in a simple SingleChildScrollView by using following snippet

```dart
Widget build(BuildContext context) {
    return Material(
        child: SingleChildScrollView(/*All of our child widgest here*/ )
    )
}
```
---

## Pushing routes

To override current page by another page and store previous one in the stack such that we can access it by performing back action just use folowing ```onPressed``` method in your button 

```dart
onPressed: () {
  Navigator.pushNamed(context, route); /
},
```

To avoid that of the stack just use the ```popAndPushNamed``` instead of ```pushnamed``` in above code

---

## !debug

To hide the debug watermark which appears on the top right corner during developing the Flutter project just add following line in your ```main.dart``` file

```dart
debugShowCheckedModeBanner: false
```

---
## Stateful vs Stateless
|  sr |stateful   | stateless|
|---|---|--
| 1  | Used when widgets are meant to change their shapes or properties   | Used when there will be no change in any of tghe widget in our page
| 2  | If main page is stateful then any of the widget can follow above property  | Either of the widget can follow the stateful properties by simply extending them e.g. TextField
| 3  | Creates 2 classes  | Creates single class
| 4 | - | Using it in specific widget improves performance

---

## Private
To make any class of variable private in our dart file simply use underscore ```_``` at  the starting of that specific variable name e.g.
```dart
String _Name = "ABC";
```

## TextField onChanged
When we type anything to the TextField and want to reflect it somewhere then use the following snippet in your TextField

```dart
onChanged: (val) {      // The changed value will be stored in this varable in String format
    name = "Welcome $val";  // Proper use of the variable
    setState(() {});}   // Rrcall the build method to refresh the current page
```
---
## Custom button using Container

We can simply create the button using container and it's properties here is  an example on how to do it 

```dart
Container(
  height: 50, // Height of the button
  width: 125, // Width of the button
  alignment: Alignment.center, // Alignment of the text on the button
  decoration: BoxDecoration( // Some decoration
    color: Colors.black12,  // Background color
    borderRadius: BorderRadius.circular(15), // Circular radius for all the corners
    border: Border.all(color: Colors.deepPurpleAccent), // Add the border on all the sides with the specified color
  ),
  child: Text( // The child of the container
    "Login",
    style: TextStyle( // Child's decoration
      color: Colors.deepPurpleAccent,
      fontWeight: FontWeight.bold,
      fontSize: 17,
    ),
  ),
)
```
To apply onClick like functions to this custom button we have to embedded that container in gestureDetector widget or in inkwell such that we can use it as our button 
- Using gestureDetector is so boring as it doesn't provide any of the feedback.
- Using inkwell provides an effect similar to ripple effect which looks more sexy.
here's illustration
```dart
InkWell(
  onTap: () {
    Navigator.popAndPushNamed(context, AllRoutes.homeRoute);
  }
  // Rest of the Container as button code
),
```
To animate the above created button change ```Container``` type to ```AnimatedContainer``` and add ```duration: Duration(seconds: 1),``` this line to it.

To add basic animation Here's the basic idea we take a boolean variable by default false value. When we click on the button the the defined variable value will be inverse by simple logic ```var=!var;``` 
and change the button properties as follows: 
```dart
(BorderRadius.circular(changeButton ? 35 : 15),
(width: changeButton ? 50 : 125,))
child: changeButton
 ? Icon(
     Icons.done,
     color: Colors.deepPurpleAccent,
   )
 : Text(
     "Login",
     style: TextStyle(
       color: Colors.deepPurpleAccent,
       fontWeight: FontWeight.bold,
       fontSize: 17,
     ),
   ),
```
such that after clicking on the button button's width will shrink to its new value as well as it's border too will be changed. You can use this too
```dart
shape: changeButton
  ? BoxShape.circle
  : BoxShape.rectangle,
```

---

## TextFormField Validation 
To validate the taken input from the TextField simply use the following property of the TextFormField
```dart
validator: (value) {
  if (value!.isEmpty) {
    return "Username cannot be empty";
  }
  return null;
}
```
but first wrap the child in the form and set key as declared key above
```dart
final _formKey = GlobalKey<FormState>();
child: Form(
                key: _formKey,
// body
)                
```
and then add check to the function which performs the further actions
```dart
if (_formKey.currentState != null && _formKey.currentState!.validate()) {}
```

---

## Drawer
Drawer is the menu bar like part of the screen which appears after clicking on the 3 bars from the left side by default. This drawer is devided in some parts like DrawerHeader.
Don't shring or wrap the text in label from drawer just truncate it
Here is the modal drawer header format

```dart
DrawerHeader(
padding: EdgeInsets.all(0),
child: //Text("Sapate Vaibhav")  // The simple text can be usd as Header only
    UserAccountsDrawerHeader(   // User Account type header
  margin: EdgeInsets.all(0),
  decoration: BoxDecoration(color: Colors.white),
  accountName: Text("Sapate Vaibhav"),  //User name
  accountEmail: Text("sapatevaibhav@duck.com"), // User email
  currentAccountPicture: CircleAvatar(
      backgroundImage: AssetImage("assets/vaibhav.png")), // User avatar
))
```

To add items in our drawer use the following template additionaly we can give actions like onTap() and more on that specific item.
```dart
 ListTile(
  leading: Icon(CupertinoIcons.home),
  title: Text("Home"),
),
```

---
## ListView
So we have done so many things now let's start some advanced things 
first of all let's try working with the ListView 
To create a basic list we can use the 
```dart 
ListView.builder( // Starting of the body
  itemCount: MyModel.items.length,  // Get the item counnt from the MyModele class
  itemBuilder: (context, index) { 
    return ItemWidget(  // Call the function which creates list items
      item: MyModel.items[index], // In MyModel class I have stored all the items in items variable
    );
  },
),
```
below is the ItemWidget class which actually creates the ListItem 
```dart
class ItemWidget extends StatelessWidget { // Class initialization
  final Item item; // declaration  of items

  const ItemWidget({super.key, required this.item}); // constructor

  @override
  Widget build(BuildContext context) { // Init the widget building
    return Card(  // This is what we want to return
      child: ListTile( // The child is ListTile which provides various features
        onTap: () { // What will happen when we tap on that specific ListItem
          print("${item.name} pressed");
        },
        tileColor: Colors.white, // Background color
        leading: Image.network(item.image), // leading means left part of thet specific tile
        title: Text(item.name), // Heading of the tile
        subtitle: Text(item.description, // Subheading of the tile
            style: TextStyle(
                fontStyle: FontStyle.italic, fontWeight: FontWeight.w200)),
        trailing: Text( // Trailing means the right part of the specific tile
          "₹ ${item.price}",
          style: TextStyle(fontWeight: FontWeight.bold, fontSize: 15),
        ),
      ),
    );
  }
}

```
Additionaly we can change the shape of the card by using ```shape: StadiumBorder()``` property to that card.


---
## hierarchy
Add this code to your dart file and see what exactly happens there and who exactly overrides and to whom.
```dart
 Center(child: Container(child: Text("Hello Bharat"),),),
    Container(
  height: 300,
  width: 300,
  color: Colors.red,
  child: Container(
    height: 50,
    width: 50,
    color: Colors.yellow,
  ),
),
```
---
## JSON
Now some things about JSON.
JSON is a file type in which we store a simple key : value paired data/ JSON files can be used to save and retrive various types of data. As well as playing with JSON files is easier than it looks so it becomes handy to store data in those files.

to load the local json file and store ut in the ```String``` we use the following code snippet.
```dart
final data = await rootBundle.loadString("assets/data/data.json");
```
Now as we have data stored in the ```String``` it is necessary to convert that data back to key : value pair (```Map```) to do this use the following line of the code
```dart
final decodedData = jsonDecode(data);
```
Now as we have the data in the format we wanted we can manipulate this data as we want.
Look here I want only items present above Map called **products** to do this wee will work on following line
```dart
final productData = decodedData["products"];
```
---
### factory
When we use final variables in the code to change their value we can use a method named ```factory``` to change it. 
To differentiate between the constructors too we use this.

Create the constructor for above JSON data stored in map using factory
```dart
factory Item.fromMap(Map<String, dynamic> map) {
```
Now store everything into a new Item such that all key : value pairs from that map will be stored their respective key from item
```dart
return Item(
      id: map["id"],
      price: map["price"],
      name: map["name"],
      description: map["description"],
      color: map["color"],
      image: map["image"]);
}
```
Now store everything in the Map again such that it can be easily accessed from any of the file by using following code
```dart
toMap() => {
  "id": id,
  "price": price,
  "name": name,
  "description": description,
  "color": color,
  "image": image
};
```
