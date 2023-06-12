# Clean Code
The following will be summaries of the chapters in Clean Code by Uncle Bob. The aim is to summarise each chapter, which will contain the key concepts of the chapter, along with examples (where applicable) that will illustrate them.

## Chapter 1: Clean Code
Let's take an example mentioned in the book, about a (nameless) company who has released a great and popular app in the 80s. They hit the ground running, the development was fast and they were making a great product; until some point. The development speed decreased, bugs were not fixed and eventually this company went out of buisness. Why? Because at the start of the project the developers didn't take the time to build a clean, maintenable system (according to one of the early stage developer of the project). Keyword being clean, as clean code makes the code base easy to change and understand. Clean code unsures that productivity will not end up plummeting.

In order to know why clean code helps with productivity, first we need to talk about what is clean code. So what is it?

According to some well known and deeply experienced programmers, clean code is elegant, efficient, does one thing well (focused), reads like a well-written prose, can be read and enhanced by a developer who is not the original author, looks like it was written by someone who cares, contains no duplication and pretty much what you expected. The common theme along most of the listed items are that the code is easy to read and is easy to change. Most of our time programming, is spent on reading code in order to add to it or enhance it. If the code is clean, it is easy to read and understand, so less time is spent on reading, which leaves more time to procude clean code. This is why productivity will not plummet in a clean code base (as long as it is kept clean).

## Chapter 2: Meaningful Names
We name our variables, our functions, our arguments, classes, and packages. We name a lot of things, actually everything we write. So we better be good at it. So, let's talk about what makes a good name.

The name should:
- Be intent revealing.
    - For example: `daysSinceModification` instead of `d` or isntead of `elapsedTime`. Notice the specification of what is being measured (daysSinceModification) and unit the of mesaurement (days).
- Not be misleading.
  - Avoid using abbreviations that have other meanings.
    - For example: using `hp`, `aix`, or `sco`in a name can be misleading as they are also names of Unix platforms or variants. 
  - Avoid using container types.
    - For example: `val accounts: Array<Account>` instead of `accountsList`. `List` is misleading and incorrect.
  - Avoid using names that wary in small ways.
    - For example: How long does it take to spot the subtle difference between  `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`? And especially when working at the end of the day this coule very easily be missread and result in a time waste.
  - Avoid using similar looking characters. 
    - For example, consider the following:
      ```
      val a = 1
      if (O == l) {
        a = O1
      } else {
        l = 01
      }
      ```
      This might not look so bad with a font that makes clear distinctions between lower-case L and 1, and upper case O (letter) and 0, but it would be very confusing if the font doesn't.
- Make a meaningful distinction from another.
  - For example: `moneyAmount` and `money`, `customerInfo` and `customer`, `message` and `theMessage`. How on earth is someone supposed to know what the differences are between thses without looking deeper? This simply results in more time being used up on understanding variable names instead of building out new code.
- Have pronouncable names
  - For example: `genymdhms` will be harder to pronounce when discussing the code with another programmer than `generationTimestamp`. 
- Be searchable
- Not be cute
  - For example: dont use `whack()` to mean `kill()`
- Not use one term for more than one purpose. This is essentially a pun.

## Chapter 3: Functions
Functions are the first building block in any program, so we should get them right. How do we do that?

The first rule is that a function should be small. The second rule is that the function should be smaller than that. Functions should do one thing and one thing only. And they should do it well. But how to know that a fucntion is doing only one thing? Let's take a look at the following example of a small functon that follows what was said above:

This function performs the inclusion of some setup and teardown pages into a test page and then renders that page into HTML.
```
fun renderPageWithSetupsAndTeardowns(
        pageData: PageData, isSuite: Boolean
    ): String? {
        if (isTestPage(pageData)) includeSetupAndTeardownPages(pageData, isSuite)
        return pageData.getHtml()
    }
```
However, one could say that the function above does 3 things:
- Determining whether the page is a test page.
- If so, including setups and teardowns.
- Rendering the page in HTML.

So which is it? Is the function doing one thing or three things? Notice that the three steps of the function are one level of abstraction below the stated name of the function. If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing. After all, the reason we write functions is to decompose a larger concept (in other words, the name of the function) into a set of steps at the next level of abstraction.

The same principle can be followed down into the function. If at each step the functions will look like the ones described above, then functions will small and there will be no duplication. 

However, a good function is not just a small function, without duplication that does one thing well. The function also should clearly express its intent (naming was discussed in Chapter 2 summary). And the less arguments the better.

## Chapter 4: Comments
Comments are not like Schindler’s List. They are not “pure good.” Indeed, comments are, at best, a necessary evil. If our programming languages were expressive enough, or if we had the talent to subtly wield those languages to express our intent, we would not need comments very much — perhaps not at all. The proper use of comments is to compensate for our failure to express ourself in code. We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration. 

Som why are comments so bad? Because they lie. Not always, and not intentionally, but too often. The older a comment is, and the farther away it is from the code it describes, the more likely it is to be just plain wrong. The reason is simple. Programmers can’t realistically maintain them. So, as a general rule of thumb, whenever there is a need for a comment, the code should be rewritten to better relate the meaning of function, class, variable, constant, etc. Comments do not make up for bad code.

Here are some example of comments in code, and how they can be improved:

```
// Returns an instance of the Responder being tested.
protected abstract fun responderInstance(): Responder?
```

Instead of writing the above comment, the fucntion could have been named `responderBeingTested`.

```
// Check to see if the employee is eligible for full benefits
if ((employee.flags && HOURLY_FLAG) && (employee.age > 65)) 
```

And instead of the comment above, the if statment can be rewritten as `if (employee.isEligibleForFullBenefits())`

However, not all comments are bad. There are legal comments which sometimes must be present, todo comments which are needed for orgonisation and some comments when expressing the intent through code was failed. Best to have no comments (and writing good code that doesn't require that). If that cannot be done, then comments can be acceptable, but that introduces a responsibilty to all developers to properly maintain the comments.

Lastly, commented out code. Do not do it. If there is uncommented code left in the codebase, it will confuse developers as to why it is there, and should it remain there. If some code is commented out, there must be a comment explaining why it is commented out, however again it introduces responsibilty for developers to maintain the comments.

## Chapter 5: Formatting

##### Vertical formatting
Let's consider a newspaper acrticle. It is read from top to bottom. At the top the headline is expected, letting the reader know what the article is about. The first paragraph gives a synopsis of the whole story. As the reader keeps on reading, the details increase until the reader is made aware of all dates, names, quotes, claims and other minutia. A source file should be no different. The name should be simple
but explanatory. The name, by itself, should be sufficient to tell the reader whether they are in the right module or not. The topmost parts of the source file should provide the high-level concepts and algorithms. Detail should increase as the reader moves downward, until at the end where they would find the lowest level functions and details in the source file.

Let's take a look at this more practically. Consider the following example:
```
class BoldWidget(parent: ParentWidget?, text: String?) : ParentWidget(parent) {

    init {
        val match: Matcher = pattern.matcher(text)
        match.find()
        addChildWidgets(match.group(1))
    }

    @Throws(Exception::class)
    fun render(): String {
        val html = StringBuffer("<b>")
        html.append(childHtml()).append("</b>")
        return html.toString()
    }

    companion object {
        const val REGEXP = "'''.+?'''"
        private val pattern: Pattern = Pattern.compile(
            "'''(.+?)'''",
            Pattern.MULTILINE + Pattern.DOTALL
        )
    }
}
```
As the reader looks at the code above, their attention is drawn to the top of each block (first line after a blank line), indicating a new thought has begun. If we were to take out the blank lines, the readability of the code drops drastically:
```
class BoldWidget(parent: ParentWidget?, text: String?) : ParentWidget(parent) {
    init {
        val match: Matcher = pattern.matcher(text)
        match.find()
        addChildWidgets(match.group(1))}
    @Throws(Exception::class)
    fun render(): String {
        val html = StringBuffer("<b>")
        html.append(childHtml()).append("</b>")
        return html.toString()}
    companion object {
        const val REGEXP = "'''.+?'''"
        private val pattern: Pattern = Pattern.compile(
            "'''(.+?)'''",
            Pattern.MULTILINE + Pattern.DOTALL
        )}
}
```

The seperate thoughts in the code start to blend together. Causing extra effort to be expended everytime the user wants to refresh their knowledge of the code.

If openess seperates concepts, then vertical density implies close association. So lines of code that are tightly related should appear vertically dense. Let's take a look at the following:
```
class ReporterConfig {
    /**
     * The class name of the reporter listener
     */
    private var className: String = ""
    /**
     * The properties of the reporter listener
     */
    private val properties = listOf<Property>()
    
    fun addProperty(property: Property) {
        properties.add(property)
    }
}
```
The comments increase the space between the 2 variables, making them seem less related to each other. And the `properties` variable now seems to be somehow to the function. If instead we had:
```
class ReporterConfig {

    private var className: String = ""
    private val properties = listOf<Property>()
    
    fun addProperty(property: Property) {
        properties.add(property)
    }
}
```
This is much easier to digest, it is more streamlined. And requires less effort to understand it. 

Concepts that are closely related should be kept vertically close to each other. Clearly this rule doesn’t work for concepts that belong in separate files. But then closely related concepts should not be separated into different files unless there is a very good reason. For those concepts that are so closely related that they belong in the same source file, their vertical separation should be a measure of how important each is to the understandability of the other. We want to avoid forcing our readers to hop around through our source files and classes.

In general function call dependencies should point in the downward direction. That is, a function that is called should be below a function that does the calling. This creates a nice flow down the source code module from high level to low level. As in newspaper articles, most important concepts come first, and are expressed with the least amount of polluting detail. Low-level details come last. This allows the reader to skim source files, getting the gist from the first few functions, without having to immerse themselfes in the details.

##### Horizontal formatting
Horizontal white space is used to associate things that are strongly related and disassociate
things that are more weakly related. Consider the following function:
```
private fun measureLine(line: String) {
    lineCount++
    val lineSize = line.length
    totalChars += lineSize
    lineWidthHistogram.addLine(lineSize, lineCount)
    recordWidestLine(lineSize)
}
```
The assignment operators are surrounded with white space to accentuate them. Assignment
statements have two distinct and major elements: the left side and the right side. The
spaces make that separation obvious. On the other hand, there are no spaces between the function name and the opening parenthesis. This is because the function and its arguments are closely related. Separating them makes them appear disjoined instead of conjoined.

A team of developers should agree upon a single formatting style, and then every member of that team should use that style.

## Chapter 6: Objects and Data Structures
What is the difference between objects and data structures? Objects hide their data behind abstractions and expose functions that operate on that data. Data structure expose their data and have no meaningful functions. Let's illustrate the above statment with a couple of examples:
First example:
```
class Point {
    var x = 0.0
    var y = 0.0
}
```
This is a data structure. It exposes data.
```
interface Point {
    val x: Double
    val y: Double

    fun setCartesian(x: Double, y: Double)
    val r: Double
    val theta: Double

    fun setPolar(r: Double, theta: Double)
}
```
This is an object, it hides the data behind a layer of abstration. It has functions to forcing the client to operate on the data in a defined way. Whereas in the `Point` class, the x and y coordinates can be set seperately. The object can have any implementation, it might be using cartesian coordinates, might use polar or some other newly invented coordinate system. One cannot tell just by looking at the object, the data structure is hidden behind a layer of abstraction. 

Another, more subtle example, is:
```
interface Vehicle {
    val fuelTankCapacityInGallons: Double
    val gallonsOfGasoline: Double
}
```
and
```
interface Vehicle {
    val percentFuelRemaining: Double
}
```
The first code snipper directly exposes the capacity and current amount of gallons, which are just getters for the variables. In the second code snippet, percentage of the fuel level is exposed, which is a layer of abstraction on `fuelTankCapacityInGallons` and `gallonsOfGasoline`.

Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes it hard to add new behaviors to existing objects. Data structures expose data and have no significant behavior. This makes it easy to add new behaviors to existing data structures but makes it hard to add new data structures to existing functions.

## Chapter 7: Error Handling
Clean code is readable, but it must also be robust. These are not conflicting goals. We can write robust clean code if we see error handling as a separate concern, something that is viewable independently of our main logic. To the degree that we are able to do that, we can reason about it independently, and we can make great strides in the maintainability of our code. Let's take a look at things that will help us do so.

When defining exception classes in an application, the most important concern should be how they are caught. Let's look at an example: 
```
val port: ACMEPort = ACMEPort(12)
        
    try {
        port.open()
    } catch (e: DeviceResponseException) {
        reportPortError(e)
        logger.log("Device response exception", e)
    } catch (e: ATM1212UnlockedException) {
        reportPortError(e)
        logger.log("Unlock exception", e)
    } catch (e: GMXError) {
        reportPortError(e)
        logger.log("Device response exception")
    } finally {
        ...
    }
```
The above statment contains a lot of duplication. This is not surpising, in most exception handling situations, the work that is done is relatively standard regardless of the actual cause. The error has to be recorded and the program should be able to proceed. Because it is known that the work that is being done is roughly the same regardless of the exception, the code can be simplified considerably by wrapping the API that is called and making sure that it returns a common exception type.
```
val port: LocalPort = LocalPort(12)

try {
    port.open()
} catch (e: PortDeviceFailure) {
    reportError(e)
    logger.log(e.getMessage(), e)
} finally {
    ...
}
```
LocalPort class is just a simple wrapper that catches and translates exceptions thrown by the ACMEPort class:
```
class LocalPort(portNumber: Int) {
    private val innerPort: ACMEPort

    init { innerPort = ACMEPort(portNumber) }

    fun open() {
        try {
            innerPort.open()
        } catch (e: DeviceResponseException) {
            throw PortDeviceFailure(e)
        } catch (e: ATM1212UnlockedException) {
            throw PortDeviceFailure(e)
        } catch (e: GMXError) {
            throw PortDeviceFailure(e)
        }
    }
}
```
Wrappers like the one defined for ACMEPort can be very useful. In fact, wrapping third-party APIs is a best practice. When a third-party API is wraped, it minimizes the
dependencies on it. The switch to a different library can happen without much penalty. Wrapping also makes it easier to mock out third-party calls when testing code. One final advantage of wrapping is that one isn’t tied to a particular vendor’s API design choices. One can define an API that suites them. In the example above, a single exception type was defined for port device failure which resulted in much cleaner code. Often a single exception class is fine for a particular area of code. The information sent with the exception can distinguish the errors. Different classes shoule be used only if the desired behaviour is to catch one excpetion, while letting another to propagate further.

Another useful tool is the special case pattern. Let’s take a look at an example. This code that sums up expenses in a billing application:
```
try {
    val expenses: MealExpenses = expenseReportDAO.getMeals(employee.getID())
    total += expenses.getTotal()
} catch (e: MealExpensesNotFound) {
    total += getMealPerDiem()
}
```
In this business, if meals are expensed, they become part of the total. If they aren’t, the employee gets a meal per diem amount for that day. The exception seperates the main buisness logic. It would be much simpler if the `getMeals` function did not throw the error. If it didn't, the code could be written like so:
```
val expenses: MealExpenses = expenseReportDAO.getMeals(employee.getID())
total += expenses.getTotal()
```
This can be achieved by changing the `ExpenseReportDAO` so that it always returns a `MealExpense` object. If there are no meal expenses, it returns a MealExpense object that returns the per diem as its total. So cleaner code can be written if the exceptions are handled at a lower level (where possible).

Do not return null. Returning null intriduces the need for not null checks and the posibility of NPEs being thrown. Consider the following code snippet:
```
val employees: List<Employee>? = getEmployees()
employees?.let { employeesNotNull ->
    employeesNotNull.forEach { employee -> totalPay += employee.pay } 
}
```
Because `getEmployees()` method can return null, we must permorn a not null check before doing anything with the list. If instead `getEmployees()` returned an empty list instead of null, then the code could be simplified to the following:
```
val employees: List<Employee> = getEmployees()
employees.forEach { totalPay += it.pay }
```

## Chapter 8: Boundaries
Often it is required to work with a thrid party API, for the sake of cleanliness of the code the boundaries must be clealy defined. Boundaries are the lines of seperation between our world (our codebase) and a thrid-party world (codebase). These boundaries may expose more that what the client wants and is concerned with. This gives more control to the client, which can lead to mistakes and bugs. 

We want to define boundaries as a layer of abstration on top of the existing boundaries. To expose only the functionality that is needed by the client. A good example of this woule be using interfaces as a boundary between our system and a thrid party library. If the library provides fine control over it's system, and those methods are directly used, then the boundaries between the thrid library system and our system blend together. Risking a need for a huge refactor job if the implementation details of the thrid party library change. However, if the boundries were defined clearly between the thrid party library and our system, (for example, through the use of an interface), then there would only be a need to change the implementation of the interface instead of changing how our system functions.

Clear boundries are also useful when working with a non existent third party library or API. The boundary would allow our system to be built and functional as it would be possible to design the interface for the non existent system to interact with ours and then to implement the existing system in such away that it would conform to our interface.
