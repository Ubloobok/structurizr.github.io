---
layout: default
title: Identifiers
parent: Structurizr DSL
nav_order: 6
permalink: /dsl/identifiers
---

# Identifiers

By default, all elements and relationships are anonymous, in that they can't be referenced from within the DSL. For example, the following statements will create a person and a software system, but neither can be referenced within the DSL. 

```
person "User"
softwareSystem "Software System"
```

To create a relationship between the two elements, we need to be able to reference them. We can do this by defining an identifier, in the same way that you'd define a variable in many programming languages.

```
p = person "User"
ss = softwareSystem "Software System"
```

Now we can use these identifiers when creating relationships, specifying which elements should be included/excluded from views, etc.

```
p -> ss "Uses"
```

Relationships can also be assigned an identifier.

```
rel = p -> ss "Uses"
```

Identifiers are only needed where you plan to reference the element/relationship. The following characters may be used when defining an identifier: `a-zA-Z_0-9`

## Identifier scope

By default, all identifiers are treated as being globally scoped, so the following will fail with an error message saying that the `api` identifier is already in use.

```
workspace {

    model {
        softwareSystem1 = softwareSystem "Software System 1" {
            api = container "API"
        }

        softwareSystem2 = softwareSystem "Software System 2" {
            api = container "API"
        }
    }
}
```

The `!identifiers` keyword allows you to specify that element identifiers should be treated as `hierarchical` (relationship identifiers are unaffected by this setting) or `flat` (the default). For example:

```
workspace {

    !identifiers hierarchical

    model {
        softwareSystem1 = softwareSystem "Software System 1" {
            api = container "API"
        }

        softwareSystem2 = softwareSystem "Software System 2" {
            api = container "API"
        }
    }
}
```
 
 Now the two API containers can be referenced via `softwareSystem1.api` and `softwareSystem2.api` respectively.
