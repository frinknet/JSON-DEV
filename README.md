JSON Definition, Expectation and Validation
===========================================

JSON-DEV is a simple specification for self-documenting JSON APIs.

JSON-DEV is a complement to JSON-P allowing validations and schema expectations
to be delivered as part of the parameter set.

JSON-DEV Basics
---------------
Successful JSON-DEV output ALWAYS contains a boolean status atribute:

```javascript
{
  "status": boolean
}
```

Successful JSON-DEV output USUALLY contains a message string or a data response.
There is no specification restricting one or the other. The only requirement is
that the message MUST be a string whereas the data can be any valid JSON data
type.

```javascript
{
  "message": string,
  "data": mixed
}
```

The message does not have any required application but may be used as an error
message displayed to a user or as a simple text explination of the process that
produced the JSON in question.

The data structured is meant to be used by an application in a manner hinted by the
schema and validation endpoints. Because of the verbose nature of these structures
they are only provided upon speciate request. When the JSON-DEV endpoint is passed
the query string variables **schema** and **validation** the addtional data
structure will also be acompanied:

```javascript
{
  "schema": mixed,
  "validation": mixed
}
```

Schema for Expectation + Validation
-----------------------------------
The data structure used for both schema and validation uses the same these takes the
form of an array with two to four items: a label string, data type, flag whether
required, and an object of specified options.

```javascript
[
  "Optional Boolean",
  "boolean"
]

[
  "Required String",
  "string",
  true
]

[
  "Optional Boolean with value names",
  "boolean",
  false,
  {
    "positive": "yes",
    "negative": "no"
  }
]
```

The actual meaning in the definition of specified types must be given by the
application. JSON-DEV is merely an encapsulation specifications any meaning for
specific data types should be provied in the defintions JSON.

Type Definitions
----------------
The JSON API should ALWAYS provide an endpoint simply named **api/definitions**
which lists all possible data types with an explanation of their options.

The data format for the definition file is an object with each type defined by an
arran with two indices, the first a string containing a textual description and the
second defining an opject full of option definitions. Option definitions also
contian an array with two indices discribing the textual definition and the default
value.

```javascript
{
  "type": ["Definition String", {
    "options": [ "Option Definition", "Default Value" ]
  } ]
}
```

See **example-definition.json** for a demonstration of what a JSON definitions file
might look like.
