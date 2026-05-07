+++
title = 'Infrastructure'
+++

# Infrastructure


What development tools did you use through process to help write code and automate the build/deployment process?

> Our software infrastructure was relatively simple compared to other medium-scale projects. We used the Love2D framework, did our programming in VSCode, and did not use LLM tools for code generation. I used the extensions "Lua" by sumneko, which provides intellisense features, type checking, and a method of documentation, "Love2D Support" by PixelByte Studios to run our program from a VSCode shortcut and link to the Love2D API, and GitHub Pull Requests to aid in the review of my teammates' code. We did not have many tools for the automation side of things, as verification is more difficult for a Love2D game project. We probably should have utilized GitHub Actions for a style checker, but we never got around to it.

What is one specific problem (e.g., debugging and issue) that you encountered while writing code and how did your tools help or hinder your ability to address that problem?

> After we pushed the dialogue functionality to main, whenever a text box was triggered to appear on screen, it would show up blank and seemingly not let the player click through to advance and dismiss it. Maya, Ian, and I looked at this during one of our weekly group meetings and spent over an hour trying to figure out what was going wrong. Because we lacked structured tools, we utilized our VSCode extensions to the best of our ability and eventually figured it out through a combination of that and old-fashioned print statements.

> We knew fairly quickly that the problem was occurring somewhere in `DialogueHandler`, so we began scanning the methods in there for anything unusual. The Lua extension came in handy because it gave us the ability for stronger type checking in a dynamically typed language. We were able to ensure that the error wasn't due to mishandling file loading or attempting to access nonexistent variables. We also managed to catch some small optimizations with the class declarations along the way. Love2D gives the option to have a standard text console, which was quite useful in the print debugging section of our work. However, our tools were not as helpful as we were hoping they would be; I finally found the issue by narrowing down execution states with printing to the console and drawing out the full function stack. The keys we were supposed to be using to mark off seen text were just getting dropped on the ground, so the program kept re-initializing the textbox every frame, hence it looking like nothing was printing.

----------

## Evidence

[Bug Fix Commit](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/commit/12d9d577c6685282761a35ac5e5afa58a067cce6) -- Ian is marked as the author, as he is the one who actually made the changes, but this was a collaborative debugging effort.