# Android Coding Standard

Android coding standards are a set of guidelines and best practices that developers should follow when writing code for Android applications. These standards help ensure that code is consistent, maintainable, and easy to read, which can make it easier to collaborate on projects and avoid common mistakes.


# File Naming
#### 1.  Class files

-   Class names are written in [UpperCamelCase](https://en.wikipedia.org/wiki/CamelCase).
-   For classes that extend an Android component, the name of the class should end with the name of the component; for example SignInActivity, SignInFragment, ImageUploaderService, ChangePasswordDialog.


#### 2. Resources files

Resources file names are written in lowercase_underscore.


#### 2.1 Drawable files


Naming conventions for drawables:

| Asset Type   	| Prefix        	| Example                  	|
|--------------	|---------------	|--------------------------	|
| Action bar   	| ab_           	| ab_stacked.9.png         	|
| Button       	| btn_          	| btn_send_pressed.9.png   	|
| Dialog       	| dialog_       	| dialog_top.9.png         	|
| Divider      	| divider_      	| divider_horizontal.9.png 	|
| Icon         	| ic_           	| ic_star.png              	|
| Menu         	| menu_         	| menu_submenu_bg.9.png    	|
| Notification 	| notification_ 	| notification_bg.9.png    	|
| Tabs         	| tab_          	| tab_pressed.9.png        	|


Naming conventions for icons

| Asset Type                      	| Prefix         	| Example                  	|
|---------------------------------	|----------------	|--------------------------	|
| Icons                           	| ic_            	| ic_star.png              	|
| Launcher icons                  	| ic_launcher    	| ic_launcher_calendar.png 	|
| Menu icons and Action Bar icons 	| ic_menu        	| ic_menu_archive.png      	|
| Status bar icons                	| ic_stat_notify 	| ic_stat_notify_msg.png   	|
| Tab icons                       	| ic_tab         	| ic_tab_recent.png        	|
| Dialog icons                    	| ic_dialog      	| ic_dialog_info.png       	|



#### 2.2 Layout files

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the SignInActivity, the name of the layout file should be activity_sign_in.xml.

| Component        	| Class Name           	| Layout Name                           	|
|------------------	|----------------------	|---------------------------------------	|
| Activity         	| UserProfileActivity  	| module_name_user_profile_activity.xml 	|
| Fragment         	| SignUpFragment       	| sign_up_fragment.xml                  	|
| Dialog           	| ChangePasswordDialog 	| change_password_dialog.xml            	|
| AdapterView item 	| —                    	| person_view_holder_item.xml           	|
| Partial layout   	| —                    	| partial_stats_bar.xml                 	|

A slightly different case is when we are creating a layout that is going to be inflated by an Adapter, e.g to populate a ListView. In this case, the name of the layout should start with item_.

Note that there are cases where these rules will not be possible to apply. For example, when creating layout files that are intended to be part of other layouts. In this case you should use the prefix partial_.



#### 2.3 Menu files

Similar to layout files, menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the UserActivity, then the name of the file should be activity_user.xml

A good practice is to not include the word menu as part of the name because these files are already located in the menu directory.


#### 2.4 Values files
Resource files in the values folder should be plural, e.g. strings.xml, styles.xml, colors.xml, dimens.xml, attrs.xml



# Code guidelines

### **Naming**

If a source file contains only a single top-level class, the file name should reflect the case-sensitive name plus the .kt extension.

Otherwise, if a source file contains multiple top-level declarations, choose a name that describes the contents of the file, apply PascalCase, and append the .kt extension.

```kotlin
// MyClass.kt

class MyClass { }
```


### **Formatting**

#### **Braces**

Braces are not required for when branches and if statement bodies which have no else if/else branches and which fit on a single line.

```kotlin
if (string.isEmpty()) return

when (value) {

    0 -> return

    // …

}
```

Braces are otherwise required for any if, for, when branch, do, and while statements, even when the body is empty or contains only a single statement.

```kotlin
if (string.isEmpty())

    return  // WRONG!


if (string.isEmpty()) {

    return  // Okay

}
```


#### **Non-empty blocks**

Braces follow the Kernighan and Ritchie style (“Egyptian brackets”) for nonempty blocks and block-like constructs:

-   No line break before the opening brace.
-   Line break after the opening brace.
-   Line break before the closing brace.
-   Line break after the closing brace, only if that brace terminates a statement or terminates the body of a function, constructor, or named class. For example, there is no line break after the brace if it is followed byelse or a comma.

```kotlin
return Runnable {

    while (condition()) {

        foo()

    }

}

return object : MyClass() {

    override fun foo() {

        if (condition()) {

            try {

                something()

            } catch (e: ProblemException) {

                recover()

            }

        } else if (otherCondition()) {

            somethingElse()

        } else {

            lastThing()

        }

    }

}

```


#### **Empty blocks**

An empty block or block-like construct must be in K&R style.


```kotlin
try {

    doSomething()

} catch (e: Exception) {} // WRONG!

try {

    doSomething()

} catch (e: Exception) {

} // Okay

```


#### **Expressions**

An if/else conditional that is used as an expression may omit braces only if the entire expression fits on one line.

```kotlin
val value = if (string.isEmpty()) 0 else 1  // Okay

val value = if (string.isEmpty())  // WRONG!

                0

            else

                1

val value = if (string.isEmpty()) { // Okay

    0

} else {

    1

}
```


#### **Indentation**

Each time a new block or block-like construct is opened, the indent increases by four spaces.

When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block.

#### **One statement per line**

Each statement is followed by a line break. Semicolons are not used.

#### **Line wrapping**

Code has a column limit of 100 characters. Except as noted below, any line that would exceed this limit must be line-wrapped, as explained below.

**Exceptions:**

-   Lines where obeying the column limit is not possible (for example, a long URL in KDoc)
-   package and import statements
-   Command lines in a comment that may be cut-and-pasted into a shell

#### **Where to break**

The prime directive of line-wrapping is: prefer to break at a higher syntactic level. Also:

-   When a line is broken at a non-assignment operator the break comes before the symbol. This also applies to the following “operator-like” symbols:
    -   The dot separator (```.```)
    -   The two colons of a member reference (```::```)
-   When a line is broken at an assignment operator the break comes after the symbol.
-   A method or constructor name stays attached to the open parenthesis (```()``` that follows it.
-   A comma (```,```) stays attached to the token that precedes it.
-   A lambda arrow (```->```) stays attached to the argument list that precedes it.

#### **Nullability**

As a rule of thumb, !! should never be used and ? should be used rarely.

Theses checks can often be avoided and doing so will provide for a more stable code-base. Whenever possible, objects and properties should be made to be not nullable.

### **Don’t ignore exceptions**

You must never do the following:

```kotlin
fun setServerPort(value: String) {  
    try {  
        serverPort = value.toInt()  
    } catch (e: NumberFormatException) {  
    
    }  
}
```


_While you may think that your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions like above creates mines in your code for someone else to trip over some day. You must handle every Exception in your code in some principled way. The specific handling varies depending on the case._ – ([Android code style guidelines](https://source.android.com/source/code-style.html))

### **Don’t catch generic exception**

You should not do this:

```kotlin
try {

    someComplicatedIOFunction();        // may throw IOException

    someComplicatedParsingFunction();   // may throw ParsingException

    someComplicatedSecurityFunction();  // may throw SecurityException

    // phew, made it all the way

} catch (e : Exception) {                 // I’ll just catch all exceptions

    handleError();                      // with one generic handler!

}
```

See the reason why and some alternatives [here](https://source.android.com/source/code-style.html#dont-catch-generic-exception)


### **Don’t use finalizers**

_There are no guarantees as to when a finalizer will be called, or even that it will be called at all. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a close() method (or the like) and document exactly when that method needs to be called. See InputStream for an example. In this case, it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs._ – ([Android code style guidelines](https://source.android.com/source/code-style.html#dont-use-finalizers))


### **Fully qualify imports**

This is bad: ```import foo.*;```

This is good: ```import foo.Bar;```

We can opt-in for this format using Android Studio Plugin.


### **Order import statements**

If you are using an IDE such as Android Studio, you don’t have to worry about this because your IDE is already obeying these rules. If not, have a look below.

The ordering of import statements is:

1.  Android imports
2.  Imports from third parties (com, junit, net, org)
3.  java and javax
4.  Same project imports

To exactly match the IDE settings, the imports should be:

-   Alphabetically ordered within each grouping, with capital letters before lower case letters (e.g. Z before a).
-   There should be a blank line between each major grouping (android, com, junit, net, org, java, javax).

More info [here](https://source.android.com/source/code-style.html#limit-variable-scope)
### **Fields definition and naming**
1. Use `val` for read-only properties and `var` for mutable properties.
2. Use lowerCamelCase for property names, starting with a lowercase letter.
3. Use descriptive names that clearly communicate the purpose of the property. Avoid abbreviations, acronyms, and single-letter names.
4. Avoid using underscores in property names, except for constants (e.g. `MAX_VALUE`).
5. If the property represents a boolean value, use a prefix like `is` or `has`. For example, `isReady` or `hasCompleted`.
6. Use backing fields for properties that require custom get or set behavior.

```kotlin
class Person {
    val firstName: String
    val lastName: String
    var age: Int
        get() = field
        set(value) {
            field = if (value >= 0) value else 0
        }

    constructor(firstName: String, lastName: String, age: Int) {
        this.firstName = firstName
        this.lastName = lastName
        this.age = age
    }
}
```


### **Limit variable scope**

_The scope of local variables should be kept to a minimum (Effective Java Item 29). By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error. Each variable should be declared in the innermost block that encloses all uses of the variable._

_Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. If you don’t yet have enough information to initialize a variable sensibly, you should postpone the declaration until you do._ – ([Android code style guidelines](https://source.android.com/source/code-style.html#limit-variable-scope))


### **Logging guidelines**

Use the logging methods provided by the Log class to print out error messages or other information that may be useful for developers to identify issues:

-   Log.v(String tag, String msg) (verbose)
-   Log.d(String tag, String msg) (debug)
-   Log.i(String tag, String msg) (information)
-   Log.w(String tag, String msg) (warning)
-   Log.e(String tag, String msg) (error)

As a general rule, we use the class name as tag and we define it as a static final field at the top of the file. For example:

```kotlin
class MyClass {  
    fun myMethod() {  
        Log.v(  
            TAG, 
            "My Method Invoked")  
    }  
  
    companion object {  
        private val TAG = MyClass::class.java.simpleName  
    }  
}
```

VERBOSE and DEBUG logs must be disabled on release builds. It is also recommended to disable INFORMATION, WARNING and ERROR logs but you may want to keep them enabled if you think they may be useful to identify issues on release builds.

If you decide to leave them enabled, you have to make sure that they are not leaking private information such as email addresses, user ids, etc.


### **Class member ordering**

There is no single correct solution for this but using a logical and consistent order will improve code learnability and readability. 

It is recommendable to use the following order:

1.  Constants
2.  Fields
3.  Constructors
4.  Override methods and callbacks (public or private)
5.  Public methods
6.  Private methods
7.  Inner classes or interfaces

```kotlin
class MyActivity : AppCompatActivity() {

    companion object {
        const val TAG = "MyActivity"
    }

    private lateinit var myTextView: TextView
    private lateinit var myAdapter: MyAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_my)

        myTextView = findViewById(R.id.my_text_view)
        myAdapter = MyAdapter()
    }

    override fun onStart() {
        super.onStart()
        Log.d(TAG, "onStart")
    }

    override fun onResume() {
        super.onResume()
        Log.d(TAG, "onResume")
    }

    override fun onPause() {
        super.onPause()
        Log.d(TAG, "onPause")
    }

    override fun onStop() {
        super.onStop()
        Log.d(TAG, "onStop")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "onDestroy")
    }

    private fun doSomething() {
        // ...
    }

    interface MyListener {
        fun onMyEvent()
    }
}
```


### **Parameter ordering in methods**

When programming for Android, it is quite common to define methods that take a Context. If you are writing a method like this, then the Context must be the first parameter.

The opposite case is callback interfaces that should always be the last parameter.

Examples:
```kotlin
// Context always goes first
fun loadUser(context: Context, userId: Int): User {
    // implementation here
}


// Callbacks always go last
fun loadUserAsync(context: Context, userId: Int, callback: UserCallback) {
    // implementation here
}

```


### **String constants, naming, and values**

Many elements of the Android SDK such as SharedPreferences, Bundle, or Intent use a key-value pair approach so it’s very likely that even for a small app you end up having to write a lot of String constants.

When using one of these components, you must define the keys as static final fields and they should be prefixed as indicated below.

| Element            	| Field Name Prefix 	|
|--------------------	|-------------------	|
| SharedPreferences  	| PREF_             	|
| Bundle             	| BUNDLE_           	|
| Fragment Arguments 	| ARGUMENT_         	|
| Intent Extra       	| EXTRA_            	|
| Intent Action      	| ACTION_           	|


### **Line length limit**

Code lines should not exceed 100 characters. If the line is longer than this limit there are usually two options to reduce its length:

-   Extract a local variable or method (preferable).
-   Apply line-wrapping to divide a single line into multiple ones.

There are two exceptions where it is possible to have lines longer than 100:

-   Lines that are not possible to split, e.g. long URLs in comments.
-   package and import statements.



#### **Line-wrapping strategies**

There isn’t an exact formula that explains how to line-wrap and quite often different solutions are valid. However, there are a few rules that can be applied to common cases.

-Break at operators

When the line is broken at an operator, the break comes before the operator. For example:

```Java
int longName = anotherVeryLongVariable + anEvenLongerOne – thisRidiculousLongOne + theFinalOne;
```
        

Assignment Operator Exception

An exception to the break at operators rule is the assignment operator =, where the line break should happen after the operator.

```java
int longName =
        anotherVeryLongVariable + anEvenLongerOne – thisRidiculousLongOne + theFinalOne;
``` 

Method chain case

When multiple methods are chained in the same line – for example when using Builders – every call to a method should go in its own line, breaking the line before the ``` . ``` 

```kotlin
// Do Not use this
Picasso.with(context).load("http://ribot.co.uk/images/sexyjoe.jpg").into(imageView);


// Use this
Picasso.with(context)

        .load("http://ribot.co.uk/images/sexyjoe.jpg")

        .into(imageView);
``` 

Long parameters case

When a method has many parameters or its parameters are very long, we should break the line after every comma ``` , ``` 

```kotlin
// Do Not use this
loadPicture(context, "http://ribot.co.uk/images/sexyjoe.jpg", mImageViewProfilePicture, clickListener, "Title of the picture");

// Use this
loadPicture(context,

        "http://ribot.co.uk/images/sexyjoe.jpg",

        mImageViewProfilePicture,

        clickListener,

        "Title of the picture");
``` 



### **Jetpack Compose Guidelines**

##### Baseline style guidelines

**Jetpack Compose framework development** MUST follow the Kotlin Coding Conventions outlined at [https://kotlinlang.org/docs/reference/coding-conventions.html](https://kotlinlang.org/docs/reference/coding-conventions.html) as a baseline with the additional adjustments described below.

##### Singletons, constants, sealed class and enum class values

**Jetpack Compose framework development** MUST name deeply immutable constants following the permitted object declaration convention of `PascalCase` as documented [here](https://kotlinlang.org/docs/reference/coding-conventions.html#property-names) as a replacement for any usage of `CAPITALS_AND_UNDERSCORES`. Enum class values MUST also be named using `PascalCase` as documented in the same section.

##### Do

```kotlin
const val DefaultKeyName = "__defaultKey"

val StructurallyEqual: ComparisonPolicy = StructurallyEqualsImpl(...)

object ReferenceEqual : ComparisonPolicy {
    // ...
}

sealed class LoadResult<T> {
    object Loading : LoadResult<Nothing>()
    class Done(val result: T) : LoadResult<T>()
    class Error(val cause: Throwable) : LoadResult<Nothing>()
}

enum class Status {
    Idle,
    Busy
}
```

##### Don't
```kotlin
const val DEFAULT_KEY_NAME = "__defaultKey"

val STRUCTURALLY_EQUAL: ComparisonPolicy = StructurallyEqualsImpl(...)

object ReferenceEqual : ComparisonPolicy {
    // ...
}

sealed class LoadResult<T> {
    object Loading : LoadResult<Nothing>()
    class Done(val result: T) : LoadResult<T>()
    class Error(val cause: Throwable) : LoadResult<Nothing>()
}

enum class Status {
    IDLE,
    BUSY
}
```

##### Naming Unit ```@Composable``` functions as entities

**Jetpack Compose framework development and Library development** MUST name any function that returns `Unit` and bears the `@Composable` annotation using `PascalCase`, and the name MUST be that of a noun, not a verb or verb phrase, nor a nouned preposition, adjective or adverb. Nouns MAY be prefixed by descriptive adjectives. This guideline applies whether the function emits UI elements or not.

###### Do
```kotlin
// This function is a descriptive PascalCased noun as a visual UI element
@Composable
fun FancyButton(text: String, onClick: () -> Unit) {
```
###### Do

```kotlin
// This function is a descriptive PascalCased noun as a non-visual element
// with presence in the composition
@Composable
fun BackButtonHandler(onBackPressed: () -> Unit) {
```

###### Don't

```kotlin
// This function is a noun but is not PascalCased!
@Composable
fun fancyButton(text: String, onClick: () -> Unit) {
```

###### Don't

```kotlin
// This function is PascalCased but is not a noun!
@Composable
fun RenderFancyButton(text: String, onClick: () -> Unit) {
```

###### Don't
```kotlin
// This function is neither PascalCased nor a noun!
@Composable
fun drawProfileImage(image: ImageAsset) {
```


##### Naming ```@Composable``` functions that return values
MUST NOT use the factory function exemption in the [Kotlin Coding Conventions for the naming of functions](https://kotlinlang.org/docs/reference/coding-conventions.html#function-names) for naming any function annotated `@Composable` as a PascalCase type name matching the function's abstract return type.

###### Do
```kotlin
// Returns a style based on the current CompositionLocal settings
// This function qualifies where its value comes from
@Composable
fun defaultStyle(): Style {
```

###### Don't

```kotlin
// Returns a style based on the current CompositionLocal settings
// This function looks like it's constructing a context-free object!
@Composable
fun Style(): Style {
```


##### Naming ```@Composable``` functions that remember {} the objects they return

MUST prefix any `@Composable` factory function that internally `remember {}`s and returns a mutable object with the prefix `remember`.

###### Do
```kotlin
// Returns a CoroutineScope that will be cancelled when this call
// leaves the composition
// This function is prefixed with remember to describe its behavior
@Composable
fun rememberCoroutineScope(): CoroutineScope {
```

###### Don't

```kotlin
// Returns a CoroutineScope that will be cancelled when this call leaves
// the composition
// This function's name does not suggest automatic cancellation behavior!
@Composable
fun createCoroutineScope(): CoroutineScope {
```


##### Compose UI API structure

Compose UI is a UI toolkit built on the Compose runtime. This section outlines guidelines for APIs that use and extend the Compose UI toolkit.

###### Compose UI elements

A `@Composable` function that emits exactly one Compose UI tree node is called an _element_.
Example

```kotlin
@Composable
fun SimpleLabel(
    text: String,
    modifier: Modifier = Modifier
) {
```

###### Elements return Unit
Elements MUST emit their root UI node either directly by calling emit() or by calling another Compose UI element function. They MUST NOT return a value. All behavior of the element not available from the state of the composition MUST be provided by parameters passed to the element function.

###### Do
```kotlin
@Composable
fun FancyButton(
    text: String,
    onClick: () -> Unit,
    modifier: Modifier = Modifier
) {
```

###### Don't
```kotlin
interface ButtonState {
    val clicks: Flow<ClickEvent>
    val measuredSize: Size
}

@Composable
fun FancyButton(
    text: String,
    modifier: Modifier = Modifier
): ButtonState {
```


###### Compose UI layouts

A Compose UI element that accepts one or more `@Composable` function parameters is called a _layout_.

Example:
```kotlin
@Composable
fun SimpleRow(
    modifier: Modifier = Modifier,
    content: @Composable () -> Unit
) {
```



###### Compose API design patterns

###### Prefer stateless and controlled @Composable functions

In this context, “stateless” refers to `@Composable` functions that retain no state of their own, but instead accept external state parameters that are owned and provided by the caller. “Controlled” refers to the idea that the caller has full control over the state provided to the composable.

###### Do
```kotlin
@Composable
fun Checkbox(
    isChecked: Boolean,
    onToggle: () -> Unit
) {
// ...

// Usage: (caller mutates optIn and owns the source of truth)
Checkbox(
    myState.optIn,
    onToggle = { myState.optIn = !myState.optIn }
)
```

###### Don't
```kotlin
@Composable
fun Checkbox(
    initialValue: Boolean,
    onChecked: (Boolean) -> Unit
) {
    var checkedState by remember { mutableStateOf(initialValue) }
// ...

// Usage: (Checkbox owns the checked state, caller notified of changes)
// Caller cannot easily implement a validation policy.
Checkbox(false, onToggled = { callerCheckedState = it })
```


###### Rules for Writing classes

You have inferred your desire for stability. Mostly this means you should aim for immutability as gaining stability through notifying composition requires a lot of work, such as was done by the creation of the `MutableState<T>` class.

###### 1. Do not use `var`s as properties inside state holding classes
As these are mutable, but do not notify composition, they will make the composables which use them unstable.

###### Do
```kotlin
data class InherentlyStableClass(val text: String)
```

###### Don't
```kotlin
data class InherentlyUnstableClass(var text: String)
```

###### 2. Private properties still affect stability

As of the time of writing, it is uncertain if this is a design choice or a bug, but let’s slightly modify our stable class from above.

```kotlin
data class InherentlyStableClass(

val publicStableProperty: String,

private var privateUnstableProperty: String

)
```

The compiler report will mark this class as unstable.
It marks both individual properties as stable, even though one is not, but marks the whole class as unstable.


###### 3. Do not use classes that belong to an external module to form state
Sadly, Compose can only infer stability for classes, interfaces, and objects that originate from a module compiled by the Compose Compiler. This means that any externally originated class will be marked as unstable, regardless of its true stability.

Let’s say you have the following class which comes from an external module and is therefore unstable:

```kotlin
class Car(

val numberOfDoors: Int,

val hasRadio: Boolean,

val isCoolCar: Boolean,

val goesVroom: Boolean

)
```

A common way to build a state using it would be to do the following:

```kotlin
data class RegisteredCarState(

val registration: String,

val car: Car

)
```

However, this is troublesome. Now you've made our state class unstable and therefore unskippable. This could potentially cause performance issues.

Luckily there are multiple ways to get around this.

If you only need a few properties of `Car` to form `RegisteredCarState`, you may simply flatten it as follows:

```kotlin
data class RegisteredCarState(

val registration: String,

var numberOfDoors: Int,

var hasRadio: Boolean

)
```

However, this may not be appropriate in cases where you need the whole object with all of its properties.

In such cases, you may create a local stable counterpart such as:

```kotlin
class CarState(

val numberOfDoors: Int,

val hasRadio: Boolean,

val isCoolCar: Boolean,

val goesVroom: Boolean

)
```

  
The two are identical, but `CarState` is stable.

Because users might need to convert to and from these classes depending on which architectural layer they are dealing with, you should provide easy mapping functions going both ways such as:

```kotlin
fun Car.toCarState(): CarState
fun CarState.toCar(): Car
```



###### 4. Do not expect immutability from collections

hings such as `List`, `Set`, and `Map` might seem immutable at first, but they are not and the Compiler will mark them as unstable.

Currently, there are two alternatives, the more straightforward one includes using  
Kotlin's [immutable collections](https://github.com/Kotlin/kotlinx.collections.immutable). However, these are still pre-release and might not be viable.

The other solution, which is a technical hack and not officially advised but used by the community, is to wrap your lists and mark the wrapper class as `@Immutable`.

```kotlin
@Immutable

data class WrappedList(

val list: List<String> = listOf()

)
```

Here the compiler still marks the individual property as unstable but marks the whole wrapper class as stable.


###### 5. Flows are unstable

Even though they might seem stable since they are observable, `Flow`s do not notify composition when they emit new values. This makes them inherently unstable. Use them only if absolutely necessary.


###### 6. Inlined Composables are neither restartable nor skippable

As with all inlined functions, these can present performance benefits. Some common Composables such as `Column`, `Row`, and `Box` are all inlined. As such this is not an admonishment of inlining Composables, just a suggestion that you should be mindful when inlining composables, or using inlined composables and be aware of how they affect the parent scope recomposition.

###### 7. Avoid running expensive calculations unnecessarily

```kotlin
@Composable

fun ConcertPerformers(venueName: String, performers: PersistentList<String>) {

val sortedPerformers = performers.sortedDescending()

Column {

Text(text = "The following performers are performing at $venueName tonight:")

LazyColumn {

items(items = sortedPerformers) { performer ->

PerformerItem(performer = performer)

}

}

}

}
```


In the above Composable, it displays the name of a venue, along with the performers who are performing at that venue. It also wants to sort that list so that the readers have an easier time finding if a performer they are interested in is performing.

However, it has one key flaw. If the venue gets changed, but the list of performers stays the same, the list will have to be sorted again. This is a potentially very costly operation. Luckily it's fairly easy to run it only when necessary.

```kotlin
@Composable

fun ConcertPerformers(venueName: String, performers: PersistentList<String>) {

val sortedPerformers = remember(performers) {

performers.sortedDescending()

}

Column {

Text(text = "The following performers are performing at $venueName tonight:")

LazyColumn {

items(items = sortedPerformers) { performer ->

PerformerItem(performer = performer)

}

}

}

}
```

In this example above, you've used `remember` that uses `performers` as a key to calculate the sorted list. It will recalculate only when the list of performers changes, sparing unnecessary recomposition.

If you have access to the original `State<T>` instance, you can reap additional benefits by deriving state directly from it, such as in the following example (please note the change function signature):

```kotlin
@Composable

fun ConcertPerformers(venueName: String, performers: State<PersistentList<String>>) {

val sortedPerformers = remember {

derivedStateOf { performers.value.sortedDescending() }

}

Column {

Text(text = "The following performers are performing at $venueName tonight:")

LazyColumn {

items(items = sortedPerformers.value) { performer ->

PerformerItem(performer = performer)

}

}

}

}
```

Here, Compose does not only skip unnecessary calculations, but is smart enough to skip recomposing the parent scope since you're only changing a locally read property and not recomposing the whole function with new parameters.


### **XML style rules**

#### **Use self closing tags**

When an XML element doesn’t have any contents, you must use self closing tags.

```XML

<!– This is Good –>

<TextView

android:id=“@+id/text_view_profile”

android:layout_width=“wrap_content”

android:layout_height=“wrap_content” />

This is bad :


<!– Don’t do this! –>

<TextView

    android:id=“@+id/text_view_profile”

    android:layout_width=“wrap_content”

    android:layout_height=“wrap_content” >

</TextView>
```


#### **Resources naming**

Resource IDs and names are written in lowercase_underscore.

#### **ID naming**

IDs should be prefixed with the name of the element in lowercase underscore. For example:

| Element   	| Prefix  	|
|-----------	|---------	|
| TextView  	| text_   	|
| ImageView 	| image_  	|
| Button    	| button_ 	|
| Menu      	| menu_   	|

#### **Strings**

String names start with a prefix that identifies the section they belong to. For example registration_email_hint or registration_name_hint. If a string doesn’t belong to any section, then you should follow the rules below:

| Prefix  	| Description                          	|
|---------	|--------------------------------------	|
| error_  	| An error message                     	|
| msg_    	| A regular information message        	|
| title_  	| A title, i.e. a dialog title         	|
| action_ 	| An action such as “Save” or “Create” 	|

#### **Styles and Themes**

Unlike the rest of the resources, style names are written in UpperCamelCase.

### **Attributes ordering in XML**

As a general rule, you should try to group similar attributes together. A good way of ordering the most common attributes is:

1.  View Id
2.  Style
3.  Layout width and layout height
4.  Other layout attributes, sorted alphabetically
5.  Remaining attributes sorted alphabetically



# Tests style rules

### **Unit tests**

Test classes should match the name of the class the tests are targeting, followed by Test. For example, if we create a test class that contains tests for the DatabaseHelper, we should name it DatabaseHelperTest.

Test methods are annotated with @Test and should generally start with the name of the method that is being tested, followed by a precondition and/or expected behaviour.

-   Template: @Test void methodNamePreconditionExpectedBehaviour()
-   Example: @Test void signInWithEmptyEmailFails()

Precondition and/or expected behaviour may not always be required if the test is clear enough without them.

Sometimes a class may contain a large number of methods, that at the same time require several tests for each method.

In this case, it’s recommendable to split up the test class into multiple ones.

For example, if the DataManager contains a lot of methods we may want to divide it into DataManagerSignInTest, DataManagerLoadUsersTest, etc. Generally, you will be able to see what tests belong together because they have common [test fixtures](https://en.wikipedia.org/wiki/Test_fixture).

### **Mockito**

Use Mockito only for mocking objects that you cannot create directly in your test code. Avoid mocking objects unnecessarily as it can make your tests less reliable.

Use descriptive method and variable names to make your test code easier to read and understand. This can help you and other developers quickly identify what the test is testing and what the expected result should be.

Use the arrange, act, assert (AAA) pattern - Use the AAA pattern to structure your test code. This pattern involves arranging the objects and data needed for the test, performing the action that you want to test, and then asserting that the expected result has been achieved.

For Example:

```kotlin
public class MyApiTest {

    @Mock
    private ApiService apiService;

    @InjectMocks
    private MyApi myApi;

    @Before
    public void setUp() {
        MockitoAnnotations.initMocks(this);
    }

    @Test
    public void testGetData() {
        // Arrange
        when(apiService.getData()).thenReturn(new Data("test"));

        // Act
        Data data = myApi.getData();

        // Assert
        assertNotNull(data);
        assertEquals("test", data.getValue());

        verify(apiService).getData();
    }
}
```


```kotlin
public class MyCalculatorTest {

    @Mock
    private MathService mathService;

    @InjectMocks
    private MyCalculator myCalculator;

    @Before
    public void setUp() {
        MockitoAnnotations.initMocks(this);
    }

    @Test
    public void testAdd() {
        // Arrange
        int x = 2;
        int y = 3;
        when(mathService.add(eq(x), eq(y))).thenReturn(5);

        // Act
        int result = myCalculator.add(x, y);

        // Assert
        assertEquals(5, result);

        verify(mathService).add(eq(x), eq(y));
    }
}
```
