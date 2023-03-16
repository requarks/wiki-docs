---
title: 模块属性
description: Structure of module properties
published: true
date: 2023-03-16T08:45:000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:34:59.676Z
---

模块属性指用户可从管理区更改的设置。

属性须以驼峰命名法明明。必须为它们分配一个`type`（类型），作为可选项，也可以为其分配 `default`（默认）值, `title`（标题）, `hint`（提示）, `enum` 列表, `multiline`和 `order`.

## 属性类型

只允许分配如下类型：

* String
* Number
* Boolean

## 示例

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

## 选项

### type

类型是**必须分配**的模块属性。它可以是属性直接值 _（如前两个示例所示）_，也可以是名为`type`的对象属性。分配的类型必须是[上面](#属性类型)列出的允许类型之一。

### default

默认值是**可选**的。如果省略，系统将根据类型推断默认值：

* String: `""` _\(empty string\)_
* Number: `0`
* Boolean: `false`

### enum

enum值是**可选**的，仅适用于String类型的属性。如果提供，它必须是字符串数组。系统将向用户显示一个下拉选择菜单，其中包含数组的值作为可能的选项。使用枚举时，还必须提供`default`值。

### title

title值是**可选**的。如果省略，系统将把属性名称开头大写作为title。

### hint

hint值是**可选**的。它显示在文本字段下方，为用户提供有用信息。如果省略，则不会显示任何提示。

### multiline

multiline值是**可选**的，仅适用于String类型的属性。如果值为`true`，系统将使用多行文本字段而非单行文本字段。如果同时指定enum与multiline属性，multiline属性将被忽略。如果省略，则回落到默认值`false`。

### order

order值是**可选**的。它控制属性的显示顺序。如果两个值具有相同顺序，则转而按definition.yml中的顺序排列。如果省略，则回落到默认值100。
