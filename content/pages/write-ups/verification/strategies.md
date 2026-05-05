+++
title = 'Testing Strategies'
+++

# Testing Strategies


According to code coverage tools, what aspects of this component are covered with tests?

> Love2d/Lua does not support code checker functionality due to the lack of formal testing. I estimate that about 40% of our codebase is covered by these tests. Our formal tests are only able to cover the per-tick update functionality, accessing various objects, and exercises the testing screen drawing code. Princess has also worked on a step-by-step guide for testing the UI to the best of our ability; it details correct behavior for the drawing states of our program, allowing us to cover that section of code too.

What kinds of tests are they?

> The formalized tests deal with the currency updates happening every tick of the game. They track basic non-negative assumptions about our currencies, as well as ensuring that dps, pps, current wood, and current paper have the values we expect as the program runs. To simplify this process and allow for more "automatic" testing, it does not allow for user input to buy weapons or actively farm wood/paper. This means that we can predict what each value should be based on the starting conditions of the test file. We created a wide range of test files to load and ensure that the updates worked properly on them.

> Here is the equals method I wrote. It forms the backbone of our testing suite, allowing us to compare floats and thus check whether our code behaves as expected.

```
-- Approximates equality of floating point numbers, used for testing calculations
equals = function(expected, actual)
    if expected == actual then
        -- Ensures this method works for 0 and small integers
        return true
    elseif expected == 0 then
        -- Just checks if actual is small
        return math.abs(actual) < 1
    elseif actual == 0 then
        -- Just checks if expected is small
        return math.abs(expected) < 1
    else
        -- Checks if the numbers are close enough, with a tolerance that scales with the size of the numbers
        return (math.abs(expected - actual) < math.max(0.1, 0.001 * expected))
    end
end
```

For code that is not covered by tests, why did you not cover them?

> The project's nature meant that it was not possible to create a comprehensive testing suite, as game execution relies on abstracted-away functions and loops from Love2D. Our game does not come with fancy physics calculations or complicated data storage, so there isn't much to poke at behind the scenes. Instead, we did what we could for ensuring the main part of execution, the repeated game loop, was as sturdy as possible.