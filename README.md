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
