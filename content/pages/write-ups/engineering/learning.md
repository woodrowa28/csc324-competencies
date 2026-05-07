+++
title = 'Self-Learning'
+++

# Self-Learning


Describe the technology that the tutorial addresses and how it fits into your project.

> Our main technology was Love2D, a Lua framework meant for programming 2D games. Since this is a pretty simple framework, we also talked about our core extensions, "Lua" by sumneko and "Love2D Support" by PixelByte Studios. Our project was a single-language endeavor, made only using Lua. Love2D is a very simple framework, giving methods to construct a core loop and draw to the screen, but not much more. This allowed us the most freedom in development and graphic design.

Evaluate how useful the tool was in your work. What were its strengths and weaknesses, especially in comparison with other tools you have used.

> Love2D was a very useful tool. It served our needs quite well, providing enough structure that we weren't floundering but still left enough room for creativity and the ability to code straight in a text editor. This is where it differs the most from other technologies that we considered; software like Unity or GameMaker have more structured systems, but they provide way more detail than we needed for our project. In particular, we did not need 3D assets or any kind of physics engine, so there was no reason to attempt to learn Unity's complicated layout. We did consider GameMaker, but ultimately, we thought it would be even harder to test code, and it focused more on the game objects and sprite system than we needed for something as graphically simple as an idle game. The extensions we used also made things much easier, preventing headaches with type mismatches or having to repeatedly check function requirements. Most of Love2D's strength came from its simplicity, but that also acts as a weakness: because it's not very comprehensive, you will inevitably be working with many other tools in the development process. This means you introduce more points for things to get mismatched, so you have to be more diligent and intentional about how everything fits together.

Identify one particular sticking point to using this technology that you would want your team to know about when adopting the tool and how you resolved it.

> I got a lot of use out of the "Love2D Support" and "Lua" extensions during development. Once they are set up properly, they provide a lot of helpful features, but getting there is a bit of a struggle. For starters, the default command for the main attraction of "Love2D Support," the ability to run your game from within VSCode, does not work by default. It overlaps with a bunch of default shortcuts and does not execute properly. Without having seen something online about this issue, we would have been very stuck. During actual programming, the Lua Language Server can only provide information about Love2D methods if you configure `.vscode/settings.json` to connect to Love2D's API. This took us a while to figure out how to do, and until we did, the extension would mark any Love2D variables or methods as undefined and would not provide any helpful documentation or parameter information.

----------

## Evidence

[Tech Talk Presentation](https://docs.google.com/presentation/d/197C0ny-cUpd18UnKOsOnp6YmsVrgBl-u1FunOaiF8gk/edit?usp=sharing)