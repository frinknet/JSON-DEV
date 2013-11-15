JSON Definition, Expectation and Validation
===========================================

JSON-DEV is a simple specification for self-documenting JSON APIs. It is intended to
aid in providing accurate API documentation using the same framework that delivers
the API. Furthermore, JSON-DEV is intended to create a standard definition of
validation criteria that can be shared between systems implemented in different
languages and tehcnologies.

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

The data structured is RECOMENDED to be used by an application in a manner hinted by
the schema and validation. JSON clients MAY use the data in a manor contrary to the
schema but MUST NOT require fields which the schema defines as optional.

Schema for Expectation + Validation
-----------------------------------
When the JSON API endpoint is passed the query string variables **schema** and
**validation** the addtional schema requested SHOULD be appended to the JSON
delivery. Because of the verbose nature of these structures they SHOULD NOT be
provided by default but only on special request.

```javascript
{
  "schema": mixed,
  "validation": mixed
}
```

The format for each validation object is an array with two REQUIRED field followed
by two OPTIONAL fields: a label string, the data type or an object containing more
validations, a flag to specify whether a field is expected or optional, and an
object of specified more advanced options.

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

NOTE:


No data type implications are prodvided in the JSON-DEV standard. JSON-DEV provides
the syntax for encapsulation of expectation and validation in a concise JSON format
suitable to be read by both machine and human.


Data Type Definitions
---------------------
Any meaning for specific data types SHOULD be provied in the defintions JSON object.
The endpoint RECOMMENDED to lists all possible data types with an explanation of
their options in **api/definitions**.

The definition object MUST contain a data object listing every type used by the API.
Each data type MUST BE defined by both string containing a textual description andan
object defining the specific options of that data type. Option definitions MUST
contain textual definition and the default value.

```javascript
{
  "status": true,
  "message": "Data Definitions",
  "data": {
    "type": [
      "Type Definition",
      {
        "options": {
          "option_name": [
            "Option Definition",
            "Default Value"
          ]
        }
      }
    ]
  }
}
```

The definitions API MAY allow a drilldown of specific types using the URI
**api/definitions/{type}** where type is the type you whish to define. When
implementing the definitions drill-down the reponse SHOULD contain the message with
a textual definition and the data with options informations.

```javascript
{
  "status": true,
  "message": "Type Definition",
  "data": {
    "option_name": [
      "Option Definition",
      "Default Value"
    ]
  }
}
```

See **example-definition.json** for complete a demonstration of a valid JSON-DEV
definition object.

JSON-DEV is a complement to JSON-P allowing validations and schema expectations
to be delivered as part of the parameter set.

