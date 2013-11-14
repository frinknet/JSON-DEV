JavaScript Object Notation for Data Expectation and Validation
==============================================================

JSON-DEV is a simple specification for self-documenting JSON APIs whether RESTful or customized. JSON-DEV
is a complement to JSON-P allowing validations and expectations to be delivered as part of the parameter set.


Basic Structure
---------------
Successful JSON-DEV output always contains this structure:

{
  "status": true,
  "data": ["mixed"]
}

Failed JSON-DEV requests return the following structure:

{
  "status": false,
  "message": "string"
}
