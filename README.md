# Tabdown
Tab markup language

## Intro
Tabdown is a simplified version of a tab layout language that lets you read and edit tab texts in the most convenient manner, but also can be transformed into more advanced languages ( HTML, iOS/Android apps, Rich Text, etc.)

The main idea behind the Tabdown syntax was to make it as easy to read as it's possible. The thing is, that Tabdown-formatted tablature can be submitted/published as a bare text like there are no special formatting tags in it. Nevertheless, text in tabs should still remain a subject to the computer processing and be a well-structured document.

The Tabdown format is a Markdown language extension, suited to make the tab and chord making process easier.

## Pros
 - Based on text input only. There's no need to use third-party editors and instruments, a simple text field is enough. This way you may be sure there won't be any malfunctions.
Minimum coding. A couple of widespread tags and a few rules is all you need to remember. Once and for all.
 - The source code is very easy to read. When you edit a tab and see the Tabdown code you can tell at first glance where chords and author commentary are. Everything is intuitive.
 - You can automatize some of the operations, like pasting repeating song parts, separating musical parts from commentaries, writing down chords with variations.
 - It's open source software that is licensed under the terms of New BSD License.
 - Applying unique definitions for each operation ( '[ ]', '#', '//' etc.) lets any Tabdown user to create a WYSIWYG editor with autocompletes. For instance, entering '#' will open a menu where you can see the list of already created sections and with one simple click you can add an entire chunk of text to a tab page. There's no need to keep the same text chunks in a source file! 
 - Flexibility - any "global variable" (e.g. "Chorus") can be overridden simply by applying the necessary adjustments.
 - The Tabdown format entails the separation of musical content and author comments visually.
 
## Cons
 - The rule that must be followed: You can't simply name a section "# Author comments" or start writing a commentary. It must be defined.
 - The only major effort that authors need to make for things to work is to follow the rules. You can think about it as a next level of creating tabs.
 - Special characters must be escaped. if you want to use one of the technical symbols, used for the Tabdown layout you must enter a backslash before them. 

## Syntax
### Chords
Chords are placed in square brackets:
```
[Am]
[Dm]     [A#]                [F]        [C]
Do you know what's worth fighting for,
[Dm]        [A#]        [F]      [C]
When it's not worth dying for?
[Dm]      [A#]        [F]      [C]
Does it take your breath away
[A#]                         [C]
And you feel yourself suffocating?
```
### Variations
If you want to mention a specific chord variation that must be applied to all the same chords in tab, use the following construction:
```
[chord]: fingering
```
For instance:
```
[G7b13]: 3x344x
```
To define two-digit frets, strings must be separated with a hyphen "-":
```
[chord]: f-i-n-g-e-r-i-n-g
```
For instance:
```
[Cadd9]: x-x-10-9-8-10
```
Besides that, a variation for a specific chord can be defined if it differs from the variations of other chords with the same name. There are 2 ways to represent a variation.defined if it differs from the variations of other chords with the same name. There are 2 ways to represent a variation.
 - Inline with chord
 - As reference in the tab legend below a tab

#### Defining variations with inline
Specific chord variations can be defined together with normal chords
```
[chord](fingering)
```
For instance:
```
[Dm](x-x-10-9-8-10)     [A#]                [F]        [C]
Do you know what's worth fighting for,
```

#### Defining variations with reference
Variation can be defined as link, which can be seen in a tab legend below a tab:
```
[chord][link_number]
  
[link_number]: fingering
```
For instance:
```
[Dm][1]     [A#]                [F][2]        [C]
Do you know what's worth fighting for,
[Dm]        [A#]        [F][2]      [C]
When it's not worth dying for?
.....
  
  
[1]: x-x-10-9-8-10
[2]: 1x323x
```

### Song sections
Song section title is words, that follow the "#" sign and non-mandatory space after it. Songs section title ends with a line break. 
```
# section
```
For instance:
```
# Verse
```
Section body is all the lines from the title of the current section to the title of the next section or the end of a song, provided there are no more sections.

### Commentaries
You should use commentary characters in order to define author commentary. 
The most important thing about a commentary is that it refers to the current song section and is not transferred to repeating song sections.
Commentaries may be onelined: 
```
// comment
```
For instance:
```
[Dm][1]     [A#]                [F][2]        [C]
Do you know what's worth fighting fоr,
// Can be played with D# instead of Dm
[Dm]        [A#]        [F][2]      [C]
When it's not worth dying fоr?
```
And multilined:
```
/*
comment
*/
```
For instance:
```
[Dm][1]     [A#]                [F][2]        [C]
Do you know what's worth fighting fоr,
/*
Can be played with D# instead of Dm
Sounds better with capo
*/
[Dm]        [A#]        [F][2]      [C]
When it's not worth dying fоr?
```

### Metadata
Metadata is defined in the following way:
```
% metaName1: value
% metaName2: value
```
For instance:
```
% tuning: E A D G B E
% capo: 2
```
To define metadata follow the following rules:
 - A line that contains metadata must start with a % symbol
 - Metadata must be written in the "key: value" format
 - There may be non-mandatory space between  % and key
 - The key and value divider (the colon ":") may contain an unlimited number of spaces before and after it
 - Metadata value must be written in the same line as key
 - All metadata must be written in a single block, line by line, without any breaks
 - There can be only one metadata block (first at the top)
 - Metadata is non-mandatory tab information. However, meta-information title (key) is restricted by the list of available values (see below). Metadata that doesn't belong to this list must be escaped.
 - Metadata may be bordered with 3 dashes at the top and bottom. E.g.
 
 ```
---
% tuning : E A D G B E
% capo   : 2
---
```

Valid key and value for metadata:

|key |values | type |  default | example |
|----|-------|------|------------|---------|
|tuning|E A D G B E|string|E A D G B E|E A D G B E|
|capo|0..100|number|0|1|
|description|<empty string>|string|<empty string>|This version is different because unlike the others it has no bar chords and has a capo on the 3rd fret. It's very easy for beginners.|
|instrument|guitar,bass,drum,ukulele,piano|string|guitar|ukulele|
|type|text,tab pro|string|text|text|
|song-part|whole song,intro,solo,chorus|string|whole song|intro|
|arrangement-type|original,author|string|original|original|
|arrangement-style|fingerstyle|string|<empty string>|fingerstyle|


### Escaping characters
If you want to use any of the technical characters that are used inTabdownlayout, place a backslash "\" before them. 
```
\[Green Day - 21 Guns\]
  
[Dm][1]     [A#]                [F][2]        [C]
Do you know what's worth fighting for,
[Dm]        [A#]        [F][2]      [C]
When it's not worth dying for?
.....
  
  
[1]: xx109810
[2]: 1x323x
```

### License
The Tabdown format is licensed under the terms of New BSD License
