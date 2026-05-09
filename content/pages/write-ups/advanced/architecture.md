+++
title = 'Architecture'
+++

# Domain-Specific Architecture (Development)

> My focus for domain-specific architecture is the class hierarchy.

What aspects of your software architecture arise because of the domain your program operates in or the technology it employs?

> Games like this often have many small objects linked to game stats and specific pieces of computation. Since Love2D is a fairly bare-bones framework, it does not have any built-in way of managing the different types of objects we wanted to use for our project. Thus, we decided to investigate an inheritance-based class system for our project.

> I spent a lot of time learning about tables, functionally Lua's only data structure, in order to work with the classes. Tables are very general structures and can hold variables, methods, and even other tables. However, the real power from metatables, which are hidden tables that define the behavior of existing tables. By manipulating the metatables of "objects," you can configure inheritance and a class hierarchy in a language that does not natively have one.

What domain-specific/technology-specific problem do your architectural choices solve?

> Since we are constructing all of the user interface ourselves, there is a lot of repetition of elements and shared properties between the parts. For example, everything on the screen needs to have coordinates and dimensions, and most things need to have defined rules and physical borders through which to be interacted with. Putting in the work to learn Lua tables and construct an Object class set up the foundation for nearly every aspect of our UI and for the different methods of production optimization. Now, we can give general guides to how a weapon purchasing button should behave and fill out our entire weapon progression with minimal changes between the buttons. We also utilized the structure to make classes for objects that we would only have 1 of, like the prestige button. Even though we didn't get the benefits of duplication, the inheritance aspect was still incredibly useful in letting us use the code for checking mouse position, hovering/clicking, and drawing with the slight tweaks we needed.

How does your solution solve these issues?

> From a usage standpoint, our class hierarchy works pretty similarly to an OO language like Java. You create new objects by calling the name of the class, can reference methods and fields attached to fields, and each instantiation exists independently of others. We cut down on a significant amount of repetition and/or inconsistent tables that would have otherwise been there. However, the behind-the-scenes construction is not as nice. Because the classes are just tables used in specific ways, you have to impose the constraints on yourself (ex. "constructors" are not a thing, you must be consistent about how you go about initializing tables). The metatable manipulation allows us to define behavior when "calling" the name of the class, which creates a new table with the same metatable information and a reference to the superclass of the object. It then returns this shell to be filled in with the specific implementations of the desired class. The documentation function from the Lua extension is also very helpful in keeping all parts connected as they should be. In all, this convoluted process gives the necessary setup for easy UI abstraction/shared behavior, as well as nicely packaging the fragments of data that are core to our game.

------------

## Resources

[Programming in Lua](https://www.lua.org/pil/contents.html)

[Classic by rxi](https://github.com/rxi/classic)

## Evidence

[Object Class](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/blob/main/classes/object.lua)

[Class Diagram](https://github.com/Idle-Devs-Progress-is-Optional/IdleDesign/blob/main/Classes%20Diagram.pdf) -- this is *very* outdated, so the structure is incredibly simplified, but most of the existing fields/methods are still present to some degree. It mainly shows the work I put into thinking about the hierarchy based on the properties of the classes and what repeated functionality we would need.

[Table-Learning Notes](https://github.com/woodrowa28/csc324-artefacts/blob/main/Lua%20Tables%20Aubrey%20Woodrow.pdf)