---
title: Module Properties
description: Structure of module properties
published: true
date: 2020-05-15T20:31:20.527Z
tags: 
---

Module properties are settings that can be changed by the user from the administration area.

A property must be in **camelCase**. They must be assigned a `type`, and optionally a `default` value, `title`, `hint`, `enum` list, `multiline`, and `order`.

## Property Types

Only the following types are allowed:

* String
* Number
* Boolean

## Example

```yaml
props:
    exampleProperty: String
    anotherProperty: Number
    propertyWithDefault:
        type: Boolean
        default: true
    propertyWithTitleHint:
        type: String
        default: 'abc'
        title: 'Property Title'
        hint: 'An explanation of the field.'
    propertyWithEnumList:
        type: String
        default: 'first'
        enum:
            - 'first'
            - 'second'
            - 'third'
    propertyWithMultiline:
        type: String
        multiline: true
```

## Options

### type

The type is **required**. It can be either the property direct value _\(as shown in the first two examples above\)_ or as an object property named `type`. Must be one of the allowed types listed [above](#property-types).

### default

The default value is **optional**. If omitted, the type default value will be inferred:

* String: `""` _\(empty string\)_
* Number: `0`
* Boolean: `false`

### enum

The enum value is **optional** and only applies to properties with type String. If provided, it must be an **array of strings**. A dropdown select will be presented to the user with the values of the array as possible choices. When using enum, the `default` value must be provided as well.

### title

The title value is **optional**. If omitted, the title will be inferred from the property name with a start case formatting applied.

### hint

The hint value is **optional**. The hint is displayed below the text field to provide the user with helpful info. If omitted, no hint will be displayed.

### multiline

The multiline value is **optional** and only applies to properties with type String. If this is `true` then a multiline textarea will be used instead of a single-line text field. If both enum and multiline properties are specified, multiline property will be ignored. If omitted, defaults to `false`.

### order

The order value is **optional**. This value controls the order in which properties are displayed. If two values have the same order, ties will be broken by the order they appear in definition.yml. If omitted, defaults to 100. 
