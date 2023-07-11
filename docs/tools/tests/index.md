# Structure map test
This is a utility to help you write tests for your structure maps using sample Questionnare Responses as test data. It provides multiple test assetions that you can use to test the map file.

**Command**
```bash
fhir-tools test [path].json
```

## Config

To test a structure map you need to create a config a json config file that has the following properties

| Property | Description                                                                                           |
| -------- | ----------------------------------------------------------------------------------------------------- |
| `type`   | The type of transformation you are currently doing str_test for tests                                 |
| `map`    | Information about the actual FML file you want to test. All you need is the path and an optional name |
| `tests`  | An array of the questionnare reponses you want to tests with this structure map                       |

Structure map config

| Element | Description |
|---|---|
| `path` | The location to the file|
| `name?` | The Src name|

The actual test array needs the following structure

| Property   | Description                                      |
| ---------- | ------------------------------------------------ |
| `response` | The path to the questinare response              |
| `verify`   | An array of the actual tests and required values |

The test section of the file needs the following

| Property      | Description                                      |
| ------------- | ------------------------------------------------ |
| `type`        | The type of assertion test you are trying to run |
| `path`        | The JSONPath to run to get the actual data       |
| `value?`      | The value to compare with                        |
| `valueRange?` | A range of values to compare with                |

Value Range

| Property | Description                                    |
| -------- | ---------------------------------------------- |
| `start`  | Starting point of the range `date` or `number` |
| `end`    | Ending point of the range `date` or `number`   |

Example file

```json
{
  "type": "str_test",
  "map": {
    "path": "./exposed_infant_hiv_test_and_results.map",
    "name": "tracing"
  },
  "tests": [
    {
      "response": "./response/positive.json",
      "verify": [
        {
          "type": "eq",
          "path": "$.resourceType",
          "value": "Bundle"
        },
        {
          "type": "lte",
          "path": "$.entry[?(@.resource.resourceType == \"Task\")].resource.code.coding[0].code",
          "value": "225368008"
        },
        {
          "type": "eq",
          "path": "$.resourceType",
          "value": "jeff"
        }
      ]
    }
  ]
}
```

## Available Test Assetions

The following operators are available:

| Operator       | Description                              |
| -------------- | ---------------------------------------- |
| `eq`           | Equal                                    |
| `eqi`          | Equal (case-insensitive)                 |
| `ne`           | Not equal                                |
| `lt`           | Less than                                |
| `lte`          | Less than or equal to                    |
| `gt`           | Greater than                             |
| `gte`          | Greater than or equal to                 |
| `in`           | Included in an array                     |
| `notIn`        | Not included in an array                 |
| `contains`     | Contains                                 |
| `notContains`  | Does not contain                         |
| `containsi`    | Contains (case-insensitive)              |
| `notContainsi` | Does not contain (case-insensitive)      |
| `null`         | Is null                                  |
| `notNull`      | Is not null                              |
| `between`      | Is between                               |
| `startsWith`   | Starts with                              |
| `startsWithi`  | Starts with (case-insensitive)           |
| `endsWith`     | Ends with                                |
| `endsWithi`    | Ends with (case-insensitive)             |
| `or`           | Joins the filters in an "or" expression  |
| `and`          | Joins the filters in an "and" expression |
| `not`          | Joins the filters in an "not" expression |
