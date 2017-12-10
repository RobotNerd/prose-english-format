# Prose Syntax - English

The Prose syntax for the English language is a way to bring aspects of
programming to the written word. It introduces syntax highlighting
and functionality to help writers visualize their stories and catch
some common mistakes early.

If you write in another language, please take the ideas here and
adapt them to your language of choice! Related projects will be included
here.

> TODO plugins that implement prose-syntax-english

> TODO
  - add notes a/b the intended usage; use LaTeX if you need something fancy

### File extension

Prose files are text-only with a file extension of `.prose`.

### Grammar

Prose documents are structured as a series of paragraphs. The rules
below describe how prose expects the writing to be structured.

- Paragraphs are separated by a blank line(s).
- Paragraphs should be left-justified, i.e. no whitespace at the
  beginning of the line.
- An indented paragraph acts as a block-quotation.
- Dialogue is placed in double quotes `"`.
  - A closing double quote closes the dialogue block.
  - If no closing quote is found, the dialogue block ends at a blank line.
- Text placed between a pair of `*` characters is *italicized*.
  - The italicized block ends at the second `*`.
  - If no closing `*` is found, the italicized block ends at the
    next blank line.
- Text placed between pairs of double underscores `__` is __bold__.
  - The bold block ends at the second `__`.
  - If no closing `__` is found, the bold block ends at the next
    blank line.
- The [Em Dash](https://en.wikipedia.org/wiki/Dash#Em_dash) is represented
  by two hyphens `--`.

### Structural markup

Special markup can be used to define document structure.

General rules:
- Tags must be left-justified.
- A tag must be on its own line.
- Multiple tags can be grouped together on contiguous lines,
  but they should be separated from paragraphs by a blank line.

Structural tags:
- Title
  - The tag `Title:` followed by the title of the work.
  - There can be only one title per project.
  - The title should be in the very first document in the .compile
    file (see the compiling section below).
  - The title should be the first line of the file where it is placed.
  - All text after the `Title:` until a line break is recognized
    as the title of the project.
- Chapter
  - The tag `Chapter:` acts the same as `Title:` unless otherwise noted.
  - There can be multiple chapter tags per project.
  - Including a chapter title is optional. In other words, a line with
    only the text `Chapter:` will act as a chapter break.
  - The chapter tag must be the first line of the file where it is placed.
- Author
  - The tag `Author:` must be followed by the name of the writer.
  - Author tags can be placed after title and chapter tags, but not with 
    section tags.
- Section
  - The tag `Section:` acts the same as `Chapter:` unless otherwise noted.
  - Sections occur within a chapter.
  - Including a section name is optional.
  - A chapter can contain multiple sections.
  - At least one blank line must be placed before the section tag, and
    at least one blank line must be placed after it.
- Section break
  - The tag `---` is a shortcut for a section tag without a title.

An example title:

```
Title: A Windy Day
Author: Mary Sue


It was a bright and windy day. The sun shone down on the grassy field...
```

An example chapter:

```
Chapter: Leaves


A gust of wind brushed past a pile of autumn leaves, kicking them up...
```

An example section, with a title:

```
...causing the doors to swing shut.


Section: Inside


The barren limbs of a sapling brushed against the glass, echoing in the...
```

Alternatively, a section break (no title) example:

```
...the fire burned out during the long, cold night.


---


The morning brought frost-covered grass on the lawn under a cold sky...
```

### Comments

Portions of the document can be marked as comments. When converting
to other formats, commented text is ignored. There are two types of
comments: line comments and block comments.

Line comments
- Begin with `##`.
- End at the next line break.
- There must be a whitespace before the `##` unless it is at the
  beginning of the line.
- Adding a backslash as a prefix `\##` will prevent it from being
  recognized as a comment.

Block comments
- Begin with `###` and end at the next `###` (or at the end of the file).
- Whitespace must occur before the opening `###` unless it is at the
  beginning of the line.
- Everything between the opening and closing comment tags is considered
  part of the comment.
- Adding a backslash as a prefix `\###` will prevent it from being
  recognized as a block comment.

### Brackets

Special notes are placed inside a pair of brackets `[]`. When converting
to other formats, the bracketed block of text is ignored.

- Begin with a `[`.
- End at `]` or the end of the file if no closing brace is found.
- Adding a backslash as a prefix will prevent the opening/closing brace
  from being recognized as a bracketed block.

### Comment tokens

Comment tokens are capitalized words that provide special metadata for
an author or editor. These tokens are recognized when placed in comments
or bracketed blocks.

These tokens are recognized:
- FIXME
- IMPORTANT
- NOTE
- TODO

### Special names

Each project can optionally have a file that defines names used in the
project. These are names of characters, places, and things unique to the
story.

- Names are stored in a file called `.names`.
- The `.names` file is stored in the root folder of the project.
- There a four categories of names that can be added to the file:
  - characters: Characters in the story.
  - places: Locations in the story.
  - things: Objects specific to the story.
  - invalid: Characters, places, or things that should not be used
    in the story. For example, a character name may have changed. By
    placing the old name in this group, it can be highlighted as an
    error in the document.
- Name patterns are added under each category header.
- The text editor must match words found in `.names` and use syntax
  highlighting to distinguish them from the surrounding text.
- A name is recognized as long as it isn't adjacent to a character
  in A-Z, a-z, 0-9, or \_.
- File format
  - There should be no leading whitespace on any line in the file.
  - Category headers
    - Each category header must be placed in braces `[]`.
    - Category names can be all uppercase, all lowercase, or the first
      letter can be capitalized.
    - The category name (in braces) must be on its only line.
    - Only the category names listed above are valid categories.
  - Name patterns
    - Name patterns are listed after the category line.
    - Name patterns are treated as regular expressions.
- Spell checking
  - When possible, patterns in `.names` should temporarily be added to
    the dictionary of the text editor. This is to ensure that these
    names are not shown as missspellings by built-in spell checkers.
  - Spell checking of these patterns should only occur for prose
    files in the same project as the `.names` file from which the
    patterns were loaded.

Example format of the `.names` file:

```
[characters]
Eric|Eric Walters
Jacob Mathers|Dr. Mathers|Mathers
Sammy

[places]
Pleasantville( High School)?
Willow Street

[things]
laser cannon
time drive

[invalid]
Jeremy
Sandra
laser rifle
```

### Syntax highlighting

Text editors that support prose should provide syntax highlighting. This is
one of the key benefits of using prose, since syntax highlighting provides
visual feedback to a writer about the structure of the document.

The following elements should be uniquely highlighted:
- Bracketed blocks
- Comments
- Comment tokens
- Dialogue
- Italicized and bolded text
- Special names
- Structure markup tags

### Folder structure

> TODO
  - ordering files for compilation

### Version control

> TODO

### Compiling files to target format

> TODO
  - .compile file
  - conversion rules
    - ignore comments and bracketed text
    - handle italics and bolded blocks
    - convert `--` to the em dash
    - collapse whitespace to single space (i.e. allow newlines in paragraphs)
  - conversion options
    - ident paragraphs vs. leave blank line between paragraphs
    - no indent on first paragraph of a section/chapter

### Best practices

> TODO
  - editor should soft wrap lines
    - line breaks inside a paragraph make it harder when editing
  - use only one blank line after every paragraph
  - enable spell-checking in your editor

### Acknowledgements

- [Fountain](https://fountain.io/)
- [GitHub Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
