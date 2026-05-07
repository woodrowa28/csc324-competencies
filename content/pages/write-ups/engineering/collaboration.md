+++
title = 'Collaboration'
+++

# Collaboration

### Instance 1 (Bug) -- [PR 90](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/pull/90/changes)

(See PR description for commit clarity)

> Work done: I moved the price calculation into its own function within the buyable objects. Whenever the item is purchased, the `buy` method then calls the `updatePrice` function. This refactoring allowed me to then call the pricing functions after the save file was loaded. Previously, the price was initialized when the empty objects were created at the very beginning of the program, but then after the save file was read and the proper item amount loaded, the price calculations was never done with the new amount until another of the item was purchased.

> Communication: We noticed that no matter what the save file looked like, the price was inaccurate for the first purchase of every item. Once you bought one, it would return to the price it should be in the progression, but the first purchase upon loading the game would always be the base price (as if you didn't own any yet). After talking with Maya about her observations of the issue, I realized it was an issue with how and when we were calculating the price. After I made the changes, she reviewed and fixed a "typo" that was not actually a typo, which we later reverted to the original state.

### Instance 2 (Submit PR) -- [PR 54](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/pull/54)

> Work done: I created the button class for purchasing a meeple. This involved programming the separate interaction coordinates for the forest vs. factory meeple, which was more complicated than other buttons; linking the purchasing to incrementing the correct meeple and updating the price; and drawing the multi-area box to the screen. I then connected the button to functionality around the codebase: it needed to be clickable via mouse click method in main and provide multiplicative bonuses to production.

> Communication: This PR did not require a ton of prior communication, as I was the one who made the original meeple and button classes and was thus familiar with their structure. I talked with Princess ahead of time and requested her review because she was in the process of drawing the graphic for the meeple button, and we needed to figure out how it should be structured. She had a couple of questions about the function of code, but the only change we made was to replace a repeated check with a local variable.

### Instance 3 (Code Review) -- [PR 94](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/pull/94)

> Work done: This was probably the most involved PR I reviewed. On the first review, I suggested some changes to reduce redundancies in the code, like calling established price updating functions and looping through item lists instead of changing each item individually. I also recommended restructuring the drawing and button clicking so the prestige button had its own class and follow existing update/drawing patterns, and subsequently edited it to be more consistent with the class documentation and structure.

> Communication: Maya requested my review after implementing the basic prestige system. The code seemed solid from the lens of correctness, but there were some "code smells" that I wanted to  clean up in order to keep our codebase as simple and neat as possible. I also noticed that the drawing code for the prestige was mostly located in main instead of abstracted away into classes like the rest of the buttons. This seemed inefficient and dissimilar to the rest of our code, so I suggested creating a new button class to hold the prestige info. Maya and I had multiple back-and-forth interactions, and thus engaged in significant collaboration for this PR.

### Instance 4 -- (Misc) [PR 112](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/pull/112)

> Work done: I reviewed Maya's PR for truncating the numbers and displaying them nicely to the screen. I noticed that one set of variables was named similarly to another property of the code. We mostly keep track of `dps` in our program, which is calculated directly from the weapon damage and meeple/prestige multipliers. `wps`, on the other hand, only exists as output for the user to see how their wood is changing per second (`dps`, then subtracting the amount taken away to make paper). We had something labeled as `dps` when it made more sense to be `wps`, so I suggested that change.

> Communication: I left a comment about the aforementioned naming issue, which Maya agreed with and changed. She added some fun printing quirks if the player somehow reached incredibly high numbers, so she wanted feedback on whether to leave them in. I found them humorous, and they do not affect our code negatively in any way, so we decided to keep them. Finally, she fixed a small issue relating to the usage of the prestige button. At the time, we had not completely developed the prestige system, so it was not a critical issue, but I thanked her for catching it because it likely saved us some trouble down the line. 

### Collaboration Difficulties?

> I did not encounter any major difficulties in the code review process. It was sometimes awkward to have to wait for code to be reviewed, especially since 1. it can be hard to stay on top of current PRs and 2. your individual progress can depend on waiting for other people to be available. Other than that, my code submissions and reviews went pretty smoothly.