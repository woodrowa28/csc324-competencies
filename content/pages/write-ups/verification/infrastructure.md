+++
title = 'Testing Infrastructure'
+++

# Testing Infrastructure


How have you automated your tests so that they both take "1-click" to run and run automatically as part of build validation?

> Because our software is a game, there is no good way to "automatically" run tests upon commit or build validation. Instead, we opted for a framework that could be toggled on and off during the execution of the game. Once in the framework, you can select a specific test in the form of a starting save file for game execution. From there, we have built-in asserts that run every frame of the game, allowing us to ensure that game updates happen as they should for a wide variety of play styles and situations.

Describe a specific occurrence in which your testing infrastructure saved you and/or your team work.

> At a high level, being able to select different "tests" from the interface (loading different save files) saved us time. This allowed us to investigate different situations without having to manually reach that point in the game. Many of these files involves states that would be very difficult to achieve through just playing the game, so it saves a lot of time to have an interface to load these without much thought. The structure also makes it very easy to add new tests: you only need to create a new txt file in the tests folder, and add a new button to the screen with the file name as a parameter.

> For a concrete example, the interface allowed me to catch the fact that the testing files were initially not hooked up correctly to the interface. Although the tracking of wood/paper on the testing interface was only added in [commit cf69d89](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/commit/cf69d8937ce86575f8e572cf395742644c5b859d), I had the code on my personal branch before that. Once I started to write per-tick functions, I noticed that a. the normal game execution was still playing out until the first test was selected, and b. the test files were not actually being loaded when their button was pressed. It would reset the timer but not load a test state. This prompted me to check our saving and loading code, revealing that the folder containing the test files was named `tests`, while the code was attempting to look into a folder named `test`. I then was more diligent in checking the other saving/loading mechanics around the test system and made it so you couldn't manually save the game using `s` during the testing mode. Technically, the regular game does still run until you hit a test, but now the display resets immediately so you don't see the wood/paper progress from the background.