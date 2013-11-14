JSON Definition, Expectation and Validation
===========================================

JSON-DEV is a simple specification for self-documenting JSON APIs. It is intended to
aid in providing accurate API documentation using the same framework that delivers
the API. Furthermore, JSON-DEV is intended to create a standard definition of
validation criteria that can be shared between systems implemented in different
languages and tehcnologies.

This specification DOES NOT define valid data type but merely the syntax for
encapsulation of definition, expectation and validation in a concise JSON format
suitable to be read by both machine and human.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt

Basics Response Objects
-----------------------
Successful JSON-DEV output MOST contains a boolean status atribute:

```javascript
{
  "status": boolean
}
```

Successful JSON-DEV output SHOULD contains a message string or a data response.
There is no specification restricting one or the other. The only requirement is
that the message MUST be a string whereas the data can be any valid JSON data
type.

```javascript
{
  "message": string,
  "data": mixed
}
```

The message MOST be a string but SHALL NOT have any required syntax definition. But
the message MAY be used as a simple text explination of a process or any other
purpose determined by the suplier of the JSON endpoints. However, the message is
RECOMENDED to be used to provide a textual error message to displayed to a user.

The data structured is RECOMENDED to be used by an application in a manner hinted by the
schema and validation. JSON clients MAY use the data in a manor contrary to the
schema but MUST NOT require fields which the schema defines as optional.

Schema for Expectation + Validation
-----------------------------------
A JSON endpoint SHOULD provide a schema for both expectation and validataion upone
request. Because of the verbose nature of these structures they are only provided
upon speciate request. When the JSON API endpoint is passed either query string
variables **schema** and **validation** the addtional schema requested should be
appended to the JSON delivery.

```javascript
{
  "schema": mixed,
  "validation": mixed
}
```

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

Data Type Definitions
---------------------
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

JSON-DEV is a complement to JSON-P allowing validations and schema expectations
to be delivered as part of the parameter set.

