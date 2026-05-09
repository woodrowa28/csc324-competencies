+++
title = 'Quality'
+++

# Quality (Engineering)

In what ways does your codebase exemplify engineering excellence? Be exhaustive as possible in your analysis.

> Our codebase has definite issues, as is inevitable with any medium- to large-scale project, but in general, it is of good quality:

> **Classes**: All of the classes in our hierarchy have Java-doc style annotations, a feature provided by the Lua extension (see bottom of page). This exemplifies good coding practice, both in terms of having a set method of documenting work and being able to quickly understand parts of the classes. Our inheritance system is set up to reduce redundancies, practicing proper principles of abstraction. The two main purposes of our classes (detailed in the 
[Medium-Scale Abstraction]({{< relref "../development/abstraction.md" >}}) 
>section) are divided by the `UIElement` and `Buyable` classes, effectively grouping together objects with similar purposes. While the number of button classes may look redundant, this is one of the better ways to go about it because each one functions so differently. All of the weapon buttons, for example, are instances of the same class because their function is the same, but the buying operation and interaction conditions are much different for something like the prestige button.

> **Architecture**: Our codebase is well-structured. We have kept `main.lua` as simple as possible by factoring most operations into separate handler files. It loads all of our classes, handles user input events per Love2D specifications, and calls our per-frame update and draw functions. We then split the work into `dialogueHandler.lua` (checks whether story conditions are met and stores the textbox drawing code), `drawingHandler.lua` (checks visibility of elements and bundles all of our drawing operations), `gameStateHandler.lua` (manages the saving and loading of files), `perSecHandler.lua` (computes the currency changes based on game dt), `soundHandler.lua` (manages the game soundtrack and sound effects), and `testingHandler.lua` (contains our tests to run each frame and the drawing code for the testing interface).

> **Variable & function naming**: our program shines in the area of specific and descriptive variable names. The only single-letter names we have are for x and y coordinates, and for constants in the price calculation equations. We have global constants declared for things like the wood to paper conversion ratio, `WOOD_TO_PAPER`, and the amount of paper sacrificed that converts to one pps, `SACRIFICE_MODIFIER`. Observe our tables for keeping track of game currencies. These are values that we constantly call back to in our code, so it is very important that we have the naming be logical and accurate, which it is.

```
    Currencies = {currentPaper = 0,
                pps = 0,
                currentWood = 0,
                dps = 0}

    PrestigeCurrencies = {globalMultiplier = 1,
                        lifetimePaper = 0,
                        lifetimeWood = 0,
                        prestige = 0}
```

> **Good dev practices**: We consistently used pull requests when making changes to the repository, allowing us to both gain practice in code review and ensure that the code we added seemed consistent with our established conventions and ideas about project execution. For example, we kept an eye out for naming conventions and efficiencies, hence why I suggested a name change for one of the variables in PR 112 of the
[Collaboration]({{< relref "../engineering/collaboration.md" >}})
> writeup. We never pushed any "breaking" changes to main, with the exception that when a new variable was added to the save file, people would have to update their personal saves to match or the code would throw a file parsing error.

> **General code cleanliness**: finally, all of these things contribute to our codebase being mostly clean and presentable. To my knowledge, we do not have any unused code remnants or stray comments, and we were intentional about how to organize and integrate the different pieces of architecture.

In what ways does it fall short? How would you addressed these issues if given more time?

> **Visibility and dialogue optimization**: I am the least happy with the code for checking when buttons should be made available to the user and for handling dialogue events. Every UI element has a parameter for whether it should be displayed to the screen and able to be interacted with. This is on by default, but we only want the upgrade buttons to be available to the players once they reach certain milestones, so we set their visibility to false and then update it to true when the conditions are met. Right now, the `dependencies` function in `DrawingHandler` checks every condition for visibility every frame. A button will never go invisible after it has been shown, so we are doing a lot of repetitive visibility checks for things whose conditions have already been met. There are also a few if-else blocks that could be replaced with switch conditionals. With more time, I would have liked to clean up this code and have tracked which checks have already been met. The checks for displaying dialogue are similarly redundant and not very scalable if we decide to add more to the story. There is also unexpected behavior--after loading the save file, the last viewed dialogue will be redisplayed. I would have liked to investigated both of these issues further to make our codebase more robust. I also have not had much of a chance to look over the sound aspects of the game, including the slider and checkbox functions, which we used an external library for. Time permitting, I would have liked to have a better understanding of the code and integrate it slightly prettier than it currently is.

> **Code formatting**: because we all have slightly different style preferences, and the code was being added to incrementally, there are some small discrepancies in naming and spacing conventions. We probably should have used a style checker, and also had more thorough discussions about style at the beginning of the semester (maybe have made a written guide?). Most notably, we have variable amounts of blank space separating code chunks, which doesn't impact the style too much but makes it slightly harder to parse at a glance.


------------

## Evidence

[Documentation PDF](https://github.com/woodrowa28/csc324-artefacts/blob/main/doc.pdf) -- The Lua extension allows you to export documentation from your code. I was expecting for it to just export for things that had the LuaLS annotations, but turns out it exports any kind of variable or method in the program. This is less helpful, as the doc is super bulky, but you can still Ctr + F to find the information of the function you're looking for.