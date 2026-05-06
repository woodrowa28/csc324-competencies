+++
title = 'Medium-Scale Abstraction'
+++

# Medium-Scale Abstraction

What functionality does your code sample abstract away?

> The class hierarchy aids in the process of abstracting away the actions that need to be performed constantly. These actions go in `love.update` and `love.draw`, both of which are repeated every tick of the game. Generally, the classes abstract away the code that would otherwise need to be repeated for drawing buttons, handling clicks, calculating DPS/PPS, and more.

How does it mechanically achieve abstraction?

> We have two main "abstract classes" (objects that are inherited from and define shared behavior but are never instantiated---no technical restrictions but they are the closest match in this invented OO programming framework): `Buyable` and `UIElement`. `Buyable` holds all the types of upgrades and items that can be purchased throughout the game, so it provides the skeleton of a `buy` method. This ensures that we can define a parameter of a button as a `Buyable` and have it be able to be "bought" no matter the underlying purchasable. `UIElement` is the superclass of everything that gets printed to the screen, so it contains fields around position, visibility, and interaction. For example, then, we can loop through our list of UI elements and call the `draw` method defined in `UIElement` regardless of the different drawing implementations for different parts.

What purpose does this abstraction serve in your larger program?

> The class structure follows a typical inheritance-based, object-oriented class hierarchy. This allows us to reduce repetition and tedious code in multiple ways: we don't need to deal with complicated drawing and position functions while displaying UI elements, and we can have the same general code to apply to many similar components of the program. We use the class hierarchy to create practically every part of the UI design, manage clickable interactions, and hold the information about the items linked to each button.

This example code demonstrates how our "abstract classes" allow for easy drawing to the screen: the exact drawing specifications are declared in the button and classes, meaning we can simply loop through a list to print everything to the screen:

```
    -- Background
    love.graphics.setColor(1, 1, 1)
    love.graphics.draw(UI.background, 0, 0)
    BackgroundButtons.help:draw()

    -- Clickable UI Buttons
    for _, weapon in pairs(WeaponButtons) do
        weapon:draw()
    end
    for _, other in pairs(OtherItemButtons) do
        other:draw()
    end
```

------------

## Evidence

[Classes folder](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/tree/main/classes)

[Class Diagram](https://github.com/Idle-Devs-Progress-is-Optional/IdleDesign/blob/main/Classes%20Diagram.pdf) -- this is *very* outdated, so the structure no longer looks like this, but most of the existing fields/methods are still present, and it shows a starting point of the hierarchy.