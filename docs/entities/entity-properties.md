---
title: Entity Properties
description: Entity properties allow data to be stored on entities without needing the use of components or attributes in the server-side of the entity, similar to block states.
category: General
mentions:
    - SirLich
    - sermah
    - MedicalJewel105
    - Luthorius
    - stirante
    - TheItsNameless
    - SmokeyStack
    - QuazChick
---

Entity properties (also known as actor properties) allow data to be stored on entities without needing the use of components or attributes (such as `minecraft:variant`) in the server-side of the entity, similar to block states.

## Entity Properties Definition

### Defining Properties on Entities

Entity Properties Definition:

<CodeHeader></CodeHeader>

```json
{
    "minecraft:entity": {
        "description": {
            "identifier": "wiki:properties_example",
            "properties": {
                "wiki:number_range_example": {
                    "values": {
                        "min": 0,
                        "max": 100
                    }
                },
                "wiki:number_enum_example": {
                    "values": [1, 2]
                },
                "wiki:string_enum_example": {
                    "values": ["first", "second", "third"]
                },
                "wiki:boolean_enum_example": {
                    "values": [true, false]
                }
            }
        }
    }
}
```

### Entity Properties Object Fields

#### `values`

:::warning
`values` property is required, and omitting this field may cause errors and failure to register the property.
:::

`values` field can be evaluated as an array of enum values, or a range of minimum and maximum values (Note that integer, float, and boolean enum values currently supports only two values):

<CodeHeader></CodeHeader>

```json
"wiki:range_example": {
    "values": {
      "min": 0,
      "max": 5
    }
}
```

**OR**

<CodeHeader></CodeHeader>

```json
"wiki:enum_example":{
    "values":[
        1,
        2
    ]
}
```

#### `default`

You can set the default value of the entity property (by default, the first value of the enum array index) through the `default` field inside the defined property object:

<CodeHeader></CodeHeader>

```json
"wiki:default_value_example":{
    "values":[
        true,
        false
    ],
    "default":false
}
```

As you can observe, the default property is set to `false` instead of `true` when the entity is spawned in the world.

#### `client_sync`

To sync through the Resource Pack (client-side), `client_sync` field can be used to allow the Client Entity access the Entity Properties. By default, the value is set to `false`.

<CodeHeader></CodeHeader>

```json
"wiki:client_sync_example": {
    "values": {
      "min": 0,
      "max": 20
    },
    "client_sync": true
}
```

### Manipulating and Accessing Entity Properties

You can access entity properties through Molang Entity Queries: - `q.property` - `q.has_property`

:::warning
These Molang Entity Queries are a part of Experimental features
:::

With entity events, you may set the entity property to a value with the `set_property` event response:

<CodeHeader></CodeHeader>

```json
"events":{
    "wiki:set_entity_property":{
        "set_property":{
            "wiki:number_enum_example":2,
            "wiki:string_enum_example":"'second'",
            "wiki:boolean_enum_example":"!q.property('wiki:boolean_enum_example')"
        }
    }
}
```

## Entity Aliases

:::danger DEPRECATED
This feature has been deprecated for format versions 1.21.10 and higher.
:::

You can define aliases for your entity to summon the entity with set entity property values through the `summon` command.
Entity can have various aliases with custom entity identifier to use:

<CodeHeader></CodeHeader>

```json
{
    "format_version": "1.16.0",
    "minecraft:entity": {
        "description": {
            "identifier": "wiki:properties_example",
            "is_spawnable": true,
            "is_summonable": true,
            "is_experimental": false,
            "properties": {
                "wiki:property_index": {
                    "client_sync": true,
                    "values": {
                        "min": 0,
                        "max": 2
                    },
                    "default": 0
                }
            },
            "aliases": {
                "wiki:default_alias": {},
                "wiki:first_alias": {
                    "wiki:property_index": 1
                },
                "wiki:second_alias": {
                    "wiki:property_index": 2
                }
            }
        }
    }
}
```

Now, the entity has multiple aliases, and you can use the defined alias identifier through the `summon` command to spawn the entity with the properties set: `/summon wiki:first_alias` will spawn the entity with the entity property `wiki:property_index` set to 1.
