# Code Review Guide


## Overall Questions

  - Is test coverage adequite?
    - How many lines of non-test code can I delete without breaking any tests?
    - Do tests cover both positive and negative scenarios?
  - Is the code DRY?
    - Is the code DRY when considering our common libraries, open source libraries, standard libraries, etc
  - Are there any (obvious) linting violations?
  - Can it be refactored?
    - Methods that look large
    - Methods that add new attributes to the object
    - Methods that are deeply nested
    - Methods that mutate passed in data
    - Methods that do not return a value
    - objects that have a lot of instance variables
    - re-declareing a parameter as a local variable
    - tests asserting against large objects
    - objects which have internal state modified in a method
  - Equality vs Inequality checks - Favor equality (avoid `if not else`)
  - Are there any events that should be logged to the Activity log?
  - Do not "do things" when handling exceptions (don't call APIs, Query the database, etc)

## Dependencies

  - lock in versions - be specific but not exact.
  - Have a conversation beforehand to make sure new dependencies are a good idea

## Python / Django

  - Can it be refactored?
    - objects that "do stuff" in the `__init__` method
    - grabbing data out of Django's request object (instead of using DRF serializers)
    - creating json by hand (instead of using DRF serializers)
    - Catching `Exception`
    - `except` with no type declared
    - global mutuable objects (including class variables and keyword argument defaults)
  - remove `self.maxDiff`s
  - remove comments (TODOs etc)
  - remove print statements
  - use `items` instead of `iteritems`
  - non Python 3 compatable code
  - using `# noqa` correctly? (use specific error code - do not use `# flake8: noqa` - that will turn off for entire file)
  - if updating code near an existing `noqa` refactor that code


## JavaScript / Ember

  - remove `console.log`s
  - remove `debugger`
  - no straight ajax calls
  - no DOM manipulation
  - use `Ember.computed` instead of `function(){}.property`
  - one `.less` file per `.hbs` file
  - are actions being logged to Google Analytics
