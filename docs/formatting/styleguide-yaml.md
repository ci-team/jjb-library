YAML style guide
================

File extension
--------------

All YAML files must have `.yaml` extension.

Indentation
-----------

This repository uses "condensed" style for yaml.
This means that no extra indent should be added for lists.

**DON'T:**

```yaml
list-enumeration:
  - item
  - item
  - item
```

```yaml
list-enumeration:
-   item
-   item
-   item
```

**DO:**

```yaml
list-enumeration:
- item
- item
- item
```

For indentation we use 2 spaces. And we don't use tabs.
Each section should have an indentation where the number of spaces is a multiple of two.

**DON'T:**

```yaml
list-enumeration:
 - item
 - item:
     key: value
```

```yaml
list-enumeration:
   - item
   - mapping:
          key: value
```

**DO:**

```yaml
list-enumeration:
- item
- item
- mapping:
    key: value
```

Brackets and braces
-------------------

Yaml is a superset of JSON, but JSON-style formatting should be avoided.

**DON'T:**

```yaml
list-enumeration: [ item , item ]
```

```yaml
mapping: { key : value }
```

**DO:**

```yaml
list-enumeration:
- item
- item
```

**DO:**

```yaml
mapping:
  key: value
```

The only exception from this rule is empty containers:

**OK:**

```yaml
empty-list: []
```

```yaml
empty-map: {}
```

Multi line strings, blocks and flow styles
------------------------------------------

When having deal with too long strings and multi-line content, use YAML blocks.

- `|` is used for cases when text contains newlines that should be kept

- `>` is used for cases when single line test is wrapped across multiple lines

**Example:**

```yaml
|
  first line
  second line
  third line
```

is equivalent for

```
first line
second line
third line
```

```yaml
>
  this 
  represents
  single 
  line
```

is equivalent for
```
this represents single line
```

**Note:** `>` and `|` could be used anywhere in YAML document:

- in root-level text

- in list items
 
- in mappings for keys and values

But multi line keys should be avoided because they reduce readability.


Logical blocks separation
-------------------------

When having deal with complex document having lot's of logical blocks, 
these blocks should be separated by extra newlines.

**Example:**

```yaml
- parameter:
    name: my-parameter
    
    parameters:
    
    - text:
        name: USER
        description: User
        
    - text:
        name: REPOSITORY
        description: Repository
        
    - text:
        name: DRY_RUN
        description: Just run check
```

When multiple entries represent single logical block, they should be grouped.

Title for such group should be provided in form of comment.

```yaml
- parameter:
    name: my-parameter
    
    parameters:
    
    # User definition
    - text:
        name: USER_NAME
        description: User's name
    - text:
        name: USER_EMAIL
        description: User's email
    - text:
        name: USER_PASSWORD
        description: User's password
```