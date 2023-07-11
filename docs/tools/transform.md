---
sidebar_position: 2
---

# StructureMap Transform

To extract data using StructureMaps we have two commands, one for working on a single Map file and a batch

- Transform questionnare response
  - This expects a structure map and QuestionnaireResponse, then transforms it using the structure maps
  ```bash
  fhir-tools transform [path].map
  ```
- Transform questionnare responses (batch)

  - This command expects a Json file that has data used to transform

  ```bash
  fhir-tools transform_batch [path].json
  ```

## Batch config

To transform QuestionnareResponses with a structure map you need to create a config a json config file that has the following properties

| Element    | Description                          |
| ---------- | ------------------------------------ |
| `type`     | The type of functionality            |
| `map`      | The Structure map config             |
| `response` | Array of questionare responses paths |

Structure map config

| Element | Description              |
| ------- | ------------------------ |
| `path`  | The location to the file |
| `name?` | The Src name             |

Example file

```json
{
  "type": "transform",
  "map": {
    "path": "./art_client_viral_load_test_results.map",
    "name": "VL_test"
  },
  "response": [
    "./response/invalid.json",
    "./response/missing.json",
    "./response/not-available.json"
  ]
}
```
