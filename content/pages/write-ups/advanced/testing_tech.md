+++
title = 'Testing Technologies'
+++

# Testing Technologies (Verification)

What advanced testing tool or technology did you employ in your code?

> Due to the lack of testing infrastructure with Love2D compatibility, we created a custom testing interface to verify how the "idle" aspects of our program ran (the background calculations logic).

What did this tool/technology validate in your program?

> The testing framework pretty much only works to test the automatic, currency per second parts of our program. It checks that pps and dps are accurate to the held weapons/sacrificed paper (values that only update when the user purchases upgrades), and that total wood and paper are linked properly and changing as we expect. The main purpose of this was to check what happens when paper per second is outpacing damage per second. If wood is abundant, paper should be increasing by the pps value, while wood is increasing by the dps value and decreasing by pps times the 5 wood needed to make one paper. The math for checking this is pretty similar to the actual calculation math, so while it is still helpful for general verification, we were not expecting this part to find many issues. If pps is outpacing the amount of wood, however, we need to make sure that paper is increasing only by the amount that the wood permits, and that wood is not being taken into the negative or having other errors.

> Paper and wood calculation code:

```
-- paper increasing how it should - constrained by the smaller of pps and dps/5 (adjusted with dt)
local expectedPaper = TestingHandler.PreviousPaper + 
    math.min(Currencies.pps * dt, ((TestingHandler.PreviousWood + Currencies.dps * dt) / WOOD_TO_PAPER))
assert(TestingHandler.equals(expectedPaper, Currencies.currentPaper), 
    "Paper should increase by the limiting factor (pps or dps / 5). Expected " .. 
    expectedPaper .. ", got " .. Currencies.currentPaper)

-- Wood changing how it should - increased with dps and decreased with pps, 
   constrained so it doesn't go negative or allow more paper to be made than the wood allows
local expectedWood = TestingHandler.PreviousWood + Currencies.dps * dt - 
    math.min(Currencies.pps * dt * WOOD_TO_PAPER, TestingHandler.PreviousWood + Currencies.dps * dt)
assert(TestingHandler.equals(expectedWood, Currencies.currentWood), 
    "Wood should change based on the difference between DPS and PPS. Expected " .. 
    expectedWood .. ", got " .. Currencies.currentWood)
```

How effective was it in this task?

> I would say that our tests were fairly effective. As mentioned above, the interface allowed us to verify behavior in "strange" and unbalanced saves. This, in conjunction with the ability to load different testing files, let us check that no matter how users played the game, the internal logic would stay accurate. The scope was not very broad, which was less than ideal, but it was effective at testing the slice of the program we wanted it to.

In what contexts did you envision yourself utilizing this tool/technology in the future?

> With more time, we would have liked to expand the scope of this to encompass more parts of our program. For example, we were hoping to get a more rigorous math system to check the precision of our calculations as the program exponentially scales. We are quite sure that user clicks are properly dealt with, as Love2D handles most of the interaction, so as nice as it would be to have more formal testing for this, Princess's testing guide is sufficient.

> Beyond this class, because we made everything ourselves and built it specifically for our game, our framework cannot be easily applied to future endeavors. However, the motivation behind the interface and the process of building it can be carried into the future. We had to be very deliberate about working within the constraints of Lua and Love2D to produce testing that made sense for our program. This knowledge will certainly benefit us in the long run for when we need to do more involved testing.


------------

## Evidence

[Testing Handler Class](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/blob/main/handlers/testingHandler.lua)

[Testing Save Files](https://github.com/Idle-Devs-Progress-is-Optional/PaperGame/tree/main/tests)