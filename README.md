Finis
=====

I'm tired of stupid INI knockoffs. Finis!


### Basic format

```
[division1]
key1=value1
key2=value2

[division2]
key1=value1
key2=value1
```

Translates to JSON as 

```json
{ "division1": { "key1":"value1", "key2":"value2" },
  "division2": { "key1":"value1", "key2":"value2" } }
```

### Subdivisions

```ini
[division1] ::
  [subdivison1]
  key1=value1
  key2=value2

  [subdivison2]
  key1=value1
  key2=value2
```

Subdivisions are indention sensitive. This allows them to be easily recognized.

### Tables

```ini
[division1]
valueA1 valueA2
valueB1 valueB2
```

Values are separate by spaces. Use double quotes if space or `=` sign is needed in values.


### Key Tables

```ini
[division1]
[key1]  [key2]
valueA1 valueA2
valueB1 valueB2
```

Values do not have to line up with columns but it is much easier to read when they do, so it is encoruaged.

### Inline Lists

```
[division1]
key1=[value1,value2]
```

Inline lists are ....

### Inline Tables

```
[division1]
key1={key1=value1,key2=value2}
```

Inline key sets ...


### Multiline values

```
[division1]
key1=|Type whatever is needed.
     |One as many line as you need.
```

or

```
[division1]
key1="""
Type whatever is needed.
One as many line as you need.
"""
```

This syntax is still a little up in the air. We'll see.


### Comments

```
; This is a comment.
```

```
# And soo is this.
```

Finis documents should use one or the other, never both. You suck if you use both.

We will consider block comments in the future, but I seriously doubt they are needed.


## Value Types

### Boolean

```
/true|false|yes|no/
```

Boolean values are distingushed by specific words, `true`, `false`, `yes` or `no`. They cannot be quotes, as that would make them strings.


### Numbers

```
/[+-]\d+([.]\d+)?(e\d+)?/
```

Number are just as you'd expect. Scientific notation is also supported.


### Dates and Times

```
/(\d\d\d\d-\d\d-\d\d(\ |T)(\d\d:\d\d(:\d\d)?))/
```

Dates are simply a sequence of digits seprated by dashes.

```
/(\d\d\d\d-\d\d-\d\d)/
```

And times are the same separated by colons.

```
/(\d\d:\d\d(:\d\d)?)/
```

They can be given together by combinung them with space or the letter `T`.

Basically this is a really simplified take on the main parts of ISO 8601.


### Strings

```
/["](.*)["]/
```

All string value *should* be in double quotes, or use the multiline notation. But undecorated strings are also acceptable as long as they cause no parsing conflicts. Undecorated string have to escape syntax.

TODO: Should all strings be in quotes, period? But then you'd just have errors when people forgot.


## Parsing Rules

* Blank lines are ignored.
* Spaces before and after `=` are ignored.


## TODO

* Is there a way to have multiline values in tables?


