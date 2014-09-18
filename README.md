

shared-api-tests
================

This repository contains a set of .json files that specify conditions for unit tests on the OT API. The specifications are intended to be used across languages, at present wrappers in R, Python,and Ruby are using them.

usage
=====

If you want curl the raw files directly you can use the raw.gihubusercontent.com link like:

```
  https://raw.githubusercontent.com/OpenTreeOfLife/shared-api-tests/master/graph_of_life.json
```

format
======

There is one file for each api (i.e. taxonomy, trns, graph\_of\_life, studies, and tree\_of\_life).

The basic format is:

```json
  "test_name": {
          "test_function": "test_function_name",
          "test_input": { dictionary_of_input },
          "tests": { dictionary_of_tests }
      },
```


test\_name
---------

A descriptive name wrapping the tests.

test\_function
-------------

The name of a wrapping function. Function names were designed to be shared across R, Python, and Ruby.  These map 1:1 with an API URL.  The naming convention is [HERE].

tests
-----

A dictionary of tests. Keys are as follows:

### contains

Tests that a key is present in the response. 

Value is an Array of Arrays. Each inner Array defines a response key and message to provide on failure of the test.

```
 ["key","message"]
```

### equals

Tests that a key in the response return a specific value.

Value is an Array of Arrays.  Each inner Array contains: 

```
 ["key", "value'], "message
```

### error

Test that <what> <raises?> an error.

Value is an Array of Arrays, each inner Array looks like

```
  ["ErrorName","message"]
```

Where ErrorName is the class in {what language} that is raised.


### length\_greater\_than

Tests that the value for a given key contains greater than N items.

Value is an Array of Arrays, each inner Array looks like

```
  ["response_key",bound_value], "message"
```

### of\type

Tests that the response provided is of the specified type.

Value is an Array with two values:

```
  [type, message]
```

At present only 'dict' is used as a type. This corresponds to a Ruby Hash.


adding a new test
=================

Fork the repo, add the test, and send us a pull request.


