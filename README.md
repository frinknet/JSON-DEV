JavaScript Object Notation for Data Expectation and Validation
==============================================================

JSON-DEV is a simple specification for self-documenting JSON APIs whether RESTful or customized. JSON-DEV
is a complement to JSON-P allowing validations and expectations to be delivered as part of the parameter set.


Basic Structure
---------------
Successful JSON-DEV output ALWAYS contains a boolean status atribute:

{
  "status": true
}

Successful JSON-DEV output USUALLY contains a message string and/or a data structure of mixed type:

{
  "message": "string",
  "data": mixed
}

When the JSON-DEV endpoint is passed the query string variables **schema** or **validation** the addtional data structure will also be acompanied:

{
  "schema": mixed,
  "validation": mixed
}

The data structure used for both of these takes the form of an array with two to four items.

    # string label
    # mixed type
    # boolean required
    # object options

For example:

[ "Optional Boolean", "boolean" ]
[ "Required String", "string", true ]
[ "Optional Boolean with value names", "boolean", false, {"positive": "yes", "negative": "no"} ]

JSON-DEV is ment as a means to encapsulate expectations for values in the data structure.
The actual definition of the specified type may be specific to the application.

Ideally, the data API should provide an endpoint named **api_url/explain_types** which lists all possible types with explanation of:

{
    status: true,
    message: "Examples of valid types",
    data: [
        "boolean": [ "Boolean variable, true or false", "boolean", {
            "positive": "positive value. Defaults to bitwise true",
            "negative": "negative value. Defaults to bitwise false",
        } ],
        "string": [ "A non-empty string", "string", {
            "values": "array of expected values"
        } ],
        "integer": [ "Any signed normal number", "integer", {
            "values": "array of expected values"
        } ],
        "float": [ "Any floating point number","float",  {
            "values": "array of expected values"
        } ],
        "[]": [ "alternate expectations", [] ],
        "{}": [ "array of objects", {}, {
            "max": "maximum number of objects in array",
            "min": "minimum number of objects in array"
        } ]
    ]
}

