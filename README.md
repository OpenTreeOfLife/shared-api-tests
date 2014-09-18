

shared-api-tests
================

This repository contains a set of .json files that specify conditions for unit tests on the OT API. The specifications are intended to be used across languages, at present wrappers in [R][2], [Python][1], and [Ruby][3] are using them.

usage
=====

See the individual language implementations for example usage.

If you want curl the raw files directly you can use the raw.gihubusercontent.com reference to an individual files like so:

```
  https://raw.githubusercontent.com/OpenTreeOfLife/shared-api-tests/master/graph_of_life.json
```

format
======

There is one file for each API: taxonomy, trns, graph\_of\_life, studies, and tree\_of\_life. Within each file there are multiple named "tests". The basic format for an individual "test" (or testing context) is:

```json
  "test_name": {
          "test_function": "test_function_name",
          "test_input": { dictionary_of_input },
          "tests": { dictionary_of_tests }
      }
```

test\_name
----------

A descriptive name wrapping a set of tests.

test\_function
--------------

The name of a wrapping function. Function names were designed to be shared across R, Python, and Ruby.  These map 1:1 with an API URL.  The naming convention is [HERE].

tests
-----

A dictionary of tests organized by type. All tests are in the format:

```
[specification, message]
```

The _message_ is the message to display when the tests *fails*.


### contains

_Tests that a key is present in the response._

Value is an Array of Arrays. Each inner Array defines a response key to check for and message to provide on failure of the test.

```json
[
 ["key","message"],
 ["other_key", "other_message']
]
```

### equals

_Tests that one or more keys in the response return a specific value._

Value is an Array of Arrays.  Each inner Array contains an array with a key/value pair, and a message.

```json
[
 [ ["key", "value'], "message" ],               
 [ ["other_key", "other_value'], "message"]    
]
```

### deep\_equals

_Tests that s in the response return a specific value._

Value is an Array of Arrays.  Each inner Array contains: 

```json
[
  [ 
   [ ["key1","key2", "key3"], "value'], "message" ]
  ],
  [
   ...
  ]
]
```

This is is translated to the test:

```
  response[key1][key2][key3] == value
```

### error

_Test that <what> <raises?> an error._

Value is an Array of Arrays, each inner Array.

```
  ["ErrorName","message"]
```

Where ErrorName is the class in {what language} that is raised.


### length\_greater\_than

_Tests that the value for a given key contains greater than N items._

Value is an Array of Arrays, each inner Array looks like

```json
[
  ["response_key",bound_value], "message"
]
```

### of\_type

_Tests that the response provided is of the specified type._

Value is an Array with two values:

```json
  [type, message]
```

At present only 'dict' is used as a type. This corresponds to a Ruby Hash.


contributing
=================

Fork the repo, add the test, [VALIDATE THE JSON][0], and send us a pull request.

licence
=======

BSD


[0]: http://jsonlint.com/
[1]: https://github.com/OpenTreeOfLife/pyopentree
[2]: https://github.com/fmichonneau/rotl
[3]: https://github.com/SpeciesFileGroup/bark 


