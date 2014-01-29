JavaScript Style Guide
======================

## Overview

- Your code should look like JavaScript, not Objective-C or Ruby

- Use single tabs for indentation

- Variables should be lowerCamelCase except for CONSTANTS, CtorFunctions, and GlobalObjects

- Temporary variables should be prefixed with a double underscore

- Object properties / methods which are not part of the Object's public API should be prefixed with a double underscore

- Don't use an insane amount of whitespace, but do use it

- Code should describe itself, there should be need of few comments

	- Event handlers should be prefixed with `handle` and suffixed with the event name (e.g. `handleClick`)

		- Also include the context if it's not obvious (e.g. `handleButtonClick` or `handleCancelClick`)

			- When the name gets too long it's a good sign the current object has too many responsibilities or that you're including too much context

- Avoid use of `querySelector` and `querySelectorAll`

- Always use curly braces when optional (e.g. `if` statements and `for` loops)

- Always use semicolons where applicable

- [Don't couple things unnecessarily](https://en.wikipedia.org/wiki/Single_responsibility_principle)

	- Avoid multiple expressions on the same line

- Most ES5 features are fair game (e.g. `Array.isArray()`, `Object.keys()`, etc.)

- Don't write browser specific code, rely on polyfills instead (and include these separately)

- Don't mutate builtin objects (polyfills are the only exception)

- Don't clutter the global namespace

	- Ensure all non-global variables are defined outside the global scope

- Use the `(function (global) {})(this)` pattern to reference the global scope


## Discussion

I'm interested in discussing the merits of each point. These guidelines are meant to promote readability and maintainability. Open an issue to discuss an improvement (please keep each issue focused on one thing, open multiple issues if needed), or submit a pull request to suggest a change.

## TODO

- Write example js files demonstrating each point (include link next to each item)

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
