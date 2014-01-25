JavaScript Style Guide
======================

## What case to use when

```javascript
// Exposed global functions must also be UpperCamelCase
global.MyFunction = function () {
};

(function () {
  // Constructor functions must be UpperCamelCase
  function MyCtor () {
  }

  // Local variables must be lower_snake_case
  var my_local_variable = 1;

  // Use UPPER_CAMEL_CASE to define constants
  // Always respect such variables by never mutating them
  var MY_CONSTANT = 42;

  // Prototype methods must be lowerCamelCase
  MyCtor.prototype.myMethod = function () {
  };

  // Local functions must also be lowerCamelCase
  function myLocalFunction () {
  }

  // Object properties must either be lower_snake_case or lowerCamelCase
  // Choose which ever one better fits the context in which it is defined

  // It's generally best to use lower_snake_case
  var obj = {
    some_property: 10
  };

  // but in contexts like DOM, lowerCamelCase is more consistent
  var other_obj = {
    className: 'some-class-name',
    nodeType: 'input'
  };
})();
```

## Other naming conventions

```javascript
(function () {

  // Prefix temporary variables with a double underscore
  // when they will be used in nested scopes
  var __my_hastable = {};

  function storeValue ( key, val ) {
    __my_hastable[key] = val;
  }

  // Prefix temporary var with a single underscore
  // when they won't be used outside of the current scope
  function map ( arr, fn ) {
    // Single character names should not be prefixed
    // and should only be used as temporary variables
    // for the current scope
    var i,
      _len = arr.length,
      _res = [];

    for ( i = 0; i < _len; i++ ) {
      res.push(
        fn( arr[i] );
      );
    }

    return res;
  }

  // Properties and methods not intended for external use
  // should be prefixed with a double underscore
  var proto = {

    get: function ( key ) {
      return this.__store[ key ];
    },

    set: function ( key, val ) {
      this.__store[ key ] = val;
    },

    reset: function () {
      this.__myPrivateMethod();
    },

    // Keep private properties and methods
    // at the bottom of the definition
    // The first thing someone should see
    // is what's available to consume
    __store: {},

    __myPrivateMethod: function () {
      this.__store = {};
    }

  };

  // Event handlers should be prefixed with `handle`
  // and suffixed with the event name
  function Foo ( el ) {
    el.addEventListener( 'click', this.handleClick.bind(this), false );
  }

  Foo.prototype.handleClick = function ( e ) {
    // do something
  };

  // Event handlers should also contain the name of
  // the object they are defined for when that is not
  // immediately obvious (i.e. the scope contains handlers
  // for multiple objects)
  function Bar ( name_el, age_el ) {
    name_el.addEventListener( 'change', this.handleNameChange, false );
    age_el.addEventListener( 'change', this.handleAgeChange, false );
  }

  Bar.prototype.handleNameChange = function ( e ) {
    // do something
  };

  Bar.prototype.handleAgeChange = function ( e ) {
    // do something
  };

  // DOM element references should be suffixed with `el`
  // and should only be named when inside of a function
  function getMyElementAttrValue ( my_el_id, attr_name ) {
    var my_el = document.getElementById(my_el_id);
    return my_el.attributes[ attr_name ].value;
  }

  getMyElementAttrValue('my_el-id');

  // or

  function getMyElementAttrValue ( my_el, attr_name ) {
    return my_el.attributes[ attr_name ].value;
  }

  getMyElementAttrValue(
    document.getElementById('my_el-id');
  );

})();
```

## Use an IDs to reference DOM nodes

`document.getElementById()` [is the fastest way](http://jsperf.com/getelementbyid-vs-queryselector) to get a reference. Use it when possible.

(Note that using a library such as [React](http://facebook.github.io/react/) will greatly improve the practicality of this by allowing you to [reference nodes](http://facebook.github.io/react/docs/more-about-refs.html#the-ref-attribute) without additional DOM reads.)


## Whitespace

There are a number of places adding a bit of whitespace makes things more readable. But don't overdo it, one space is enough.

```javascript
// Good
function myFunction ( arg_1, arg_2, arg_3 ) {
  var obj = {};
  obj[ arg_1 ] = [ arg_2, arg_3 ];
}

// Also good
function myFunction (arg_1, arg_2, arg_3) {
  var obj = {};
  obj[arg_1] = [arg_2, arg_3];
}

// Bad
function myFunction (     arg_1, arg_2, arg_3     ) {
  var obj     =     {};
  obj[    arg_1    ] = [    arg_2, arg_3    ];
}

// Also bad
function myFunction(arg_1,arg_2,arg_3){var obj={};obj[arg_1]=[arg_2,arg_3];}
```

### Indentation

Use Tabs.

Tabs vs spaces seems to be a never ending argument. Seeing as it's very easy to display tabs as how ever many spaces you prefer, and doing the same with spaces is more difficult (matching only those at the beginning of lines, etc.), it's very hard to see why spaces would be preferred.

The only time spaces would be 'better' is when viewing the code in plain text in a setting where you do not have control over the width of each tab. If this really annoys you there are several options to choose from: 1) Copy it into your favourite editor, 2) Replace all the tabs with n spaces, 3) Install a browser plugin to replace all the tabs with n spaces as this is likely the context in which you are in.

## Misc.

When in doubt, stop and consider if one way is more explicit than the other. You shouldn't be writing overly verbose code (you're writing JavaScript, not Objective-C), but it's often too easy to go running in the other direction.

```javascript
// As a general rule, code within any given context or scope
// should not be verbose about that context or scope.
// It should however be self evident once the context or scope is realized.
function Person (name) {
  this.__name = name;
}

// overly verbose
Person.prototype.getPersonName = function () {
  return this.__name;
};

// not verbose enough
Person.prototype.name = function () {
  return this.__name;
};

// do this instead
Person.prototype.getName = function () {
  return this.__name;
};

// Empty / non-empty array checks

var arr = [];

// Check that array has length > 0
if (arr.length) {
  // do something
}

// Check that array has length of 0
if (arr.length === 0) {
  // do something
}

// This is another common way of doing this
// but `!` is harder to see than ` === 0`
// and both have ~ the same performance
// Please avoid doing it this way
if (!arr.length) {
  // do something
}

// Type checking

// In general use typeof variable === 'type'
typeof variable === 'string';
typeof variable === 'number';
typeof variable === 'object';
typeof variable === 'undefined';

// But arrays are different,
// avoid common complexities and use
Array.isArray( variable );

// And checking if a local var is undefined can be better done like this
local_var === undefined

// Avoid using == to check for null or undefined
// This is not explicit and may not be immediately obvious to the reader
// Do two separate checks instead
local_var === null || local_var === undefined

// However, needing to check for null or undefined is a code smell
// and you should look into refactoring your code so such a check
// is no longer needed, for example:
var local_var = null;

// instead of
var local_var;

// Always use {} for if statements, even when it can be easily written without
if (local_var === null) {
  return;
}

// Always memoize array.length in for loops
for (var i = 0, _len = arr.length; i < _len; i++) {
  // do something
}
```
