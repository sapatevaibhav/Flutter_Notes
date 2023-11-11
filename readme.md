# Flutter 

Notes taken by me during learning Flutter...

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
      'assets/completion.png',
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
## custom button using Container

We can simply create the button using container and it's properties here is  an example on how to do it 

```dart
Container(
  height: 50,
  width: 125,
  alignment: Alignment.center,
  decoration: BoxDecoration(
    color: Colors.black12,
    borderRadius: BorderRadius.circular(15),
    // border: Border.all(1)
  ),
  child: Text(
    "Login",
    style: TextStyle(
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

--- 

