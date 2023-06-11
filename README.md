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

## Chapter 7: Error Handling

## Chapter 8: Boundaries
