+++
title = 'Medium-Scale Architecture'
+++

# Medium-Scale Architecture


What architectural pattern does your program employ?

> Our program includes multiple "handler" files that define specific event behavior. In order to keep `main.lua` easy to read, all of the major activities and event results are hosted in separate files, each with their own specialization. I created the tick/second updates (`perSecHandler.lua`), worked with Ian on testing (`testingHandler.lua`), helped with the dialogue and drawing (`dialogueHandler.lua` and `drawingHandler.lua` respectively), and did not contribute much to the game saving/loading handler (`gameStateHandler.lua`).

> The most independent of these handlers is the testing one, as it controls an entirely separate interface used only for our testing suite. It deviates from the general architecture of our program the most; updates and printing to the screen still happen, but the updates are behind the scenes and include `assert` tests, the testing interface is drawn, and the user cannot impact the test gameplay (only select different tests or exit the interface).

What components result from this pattern in your program?

> This pattern handles both the "update" and "draw" sections of Love2D's core loop, with different handlers specializing in different areas.

What technologies and/or libraries make-up each of the components?

> No other technologies are utilized in these components, as our codebase is solely in Lua and relies very minimally on outside repositories.

------------

## Evidence

[Handlers folder](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/tree/main/handlers)