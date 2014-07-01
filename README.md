FINIS
=====

I'm tired of stupid INI knockoffs. FINIS!


### Basic Format

```
[division1]
key1=value1
key2=value2

[division2]
key1=value1
key2=value1
```

```json
{ "division1": { "key1":"value1", "key2":"value2" },
  "division2": { "key1":"value1", "key2":"value2" } }
```

Yea, this is just INI.


### Subdivisions

```
[division1]
  [subdivison1]
  key1=value1
  key2=value2

  [subdivison2]
  key1=value1
  key2=value2
```

```json
{ "division1": { "subdivision1": { "key1":"value1", "key2":"value2" },
                 "subdivision2": { "key1":"value1", "key2":"value2" } } }
```

Subdivisions are indention sensitive. This allows them to be easily recognized.

NOTE: THe alternate approach, if we don't want indention, is to use double brackets.

```
[division1]

[[subdivison1]]
key1=value1
key2=value2

[[subdivison2]]
key1=value1
key2=value2
```


### Tables

```
[division1]
valueA1 valueA2
valueB1 valueB2
```

```json
{ "division1": [ [ "valueA1", "valueA2" ],
                 [ "valueB1", "valueB2" ] ] }
```

Values are separate by spaces. Use double quotes if space or `=` sign is needed in values.


### Key Tables

```
[division1]
[key1]  [key2]
valueA1 valueA2
valueB1 valueB2
```

```json
{ "division1": [ { "key1":"valueA1", "key2":"valueA2" },
                 { "key1":"valueB1", "key2":"valueB2" } ]
```

**TODO: There may be too much ambiguity here, as it disallows single column key tables.**

Values do not have to line up with columns but it is much easier to read when they do, so it is encoruaged.


### Inline Lists

```
[division1]
key1=[valueA1,valueA2]
key2=[valueB1,valueB2]

```

```json
{ "division1": { "key1": [ "valueA1", "valueA2" ],
                 "key2": [ "valueB1", "valueB2" ] } }
```


Inline lists are are command separated values enclosed in square brackets.


### Inline Tables

```
[division1]
key1={keyA1=valueA1,keyA2=valueA2}
key2={keyB1=valueB1,keyB2=valueB2}
```

```json
{ "division1": { "key1": { "keyA1": "valueA1", "keyA2": "valueA2" }, 
                 "key2": { "keyA1": "valueA1", "keyA2": "valueA2" } } }
```

Inline key sets are key-value pairs seprated by commas and enclosed in curly brackets.


### Multiline Values

```
[division1]
key1="Type whatever you want.
     "As many lines as you need.
```

(NOTE: I first considered `|` instead of `"`. Would that be better?)

or

```
[division1]
key1="Type whatever you want."
     "As many lines as you need."
```

```json
{ "division1": { "key1": "Type whatever is needed.\nAs many lines as you need." } }
```

**TODO: This syntax is still a little up in the air. We'll see.**

Multline values ...


### Outboard Multiline Strings

```
["divison1"]
Type whatever you want.
As many lines as you need.
```

```json
{ "division1": "Type whatever is needed.\nAs many lines as you need." }
```

Multiline values are strings...

Square brackets at the start of line need to be escaped.

TODO: Can this be generaized to all types? Should it?


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


