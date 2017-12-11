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

### Configuration file

Each prose project can optionally include a configuration file specific to
that project. All of the following formats should be supported:
- json
- yaml

The configuration file should be named `config.*` with the appropriate file
extension based on the file format (e.g. `config.json`, `config.yml`, etc).
However, text editors that support prose should fallback to autodetecting
the file format when possible.

The configuration file can contain:
- project compilation options
- special names used in the project

Available configuration options are detailed in the subsections below.

> TODO reference the folder structure section below

#### Configuration: special names

Each project can optionally add names used in the project to the configuration
file. These are the names of characters, places, and things unique to
the story. Text editors can use syntax highlighting to make these names
visually distinct from the surrounding text. This helps writers to
quickly figure out when they misspell a character name or use the
wrong name in a story.

Rules
- Names are stored in a `names` section of the config file.
- There a four categories of names that can be added to the config file:
  - Characters: Characters in the story.
  - Places: Locations in the story.
  - Things: Objects specific to the story.
  - Invalid: Characters, places, or things that should not be used
    in the story. For example, a character name may have changed during
    the course of rewriting a story. By placing the old name in this group,
    it can be highlighted as an error in the document.
- A list of name patterns is added under each category header.
- The text editor must match words in the names lists and use syntax
  highlighting to distinguish these patterns from the surrounding text.
  - When possible, the highlighting used for the groups of characters,
    places, and things should be visually distinct from each other.
    (For example, all character names might be bold, places underlined, and
    things italicized.)
  - When possible, items in the invalid group should be highlighted as errors.
- A name is recognized as long as it isn't adjacent to any of these characters:
  - A-Z
  - a-z
  - 0-9
  - \_
- Name patterns
  - Name patterns are added as a list of values under the appropriate section.
  - Each name pattern is treated as a regular expression.
- Spell checking
  - When possible, name patterns should temporarily be added to
    the dictionary of the text editor. This is to ensure that these
    names are not shown as misspellings by built-in spell checkers.
  - Spell checking of these patterns should only occur for prose
    files in the same project as the configuration file from which the
    name patterns were loaded.

An example names section for `config.json`:

```json
{
  "names": {
    "characters": [
      "Eric|Eric Walters",
      "Jacob Mathers|Dr. Mathers|Mathers",
      "Sammy"
    ],
    "places": [
      "Pleasantville( High School)?,"
      "Willow Street"
    ],
    "things": [
      "laser cannon,"
      "time drive"
    ],
    "invalid": [
      "Jeremy",
      "Sandra",
      "laser rifle"
    ]
  }
}
```

An example names section for `config.yml`:

```yaml
---
names:
  characters:
    - Eric|Eric Walters
    - Jacob Mathers|Dr. Mathers|Mathers
    - Sammy
  places:
    - Pleasantville( High School)?
    - Willow Street
  things:
    - laser cannon
    - time drive
  invalid:
    - Jeremy
    - Sandra
    - laser rifle
```

#### Configuration: project compilation options

> TODO
  - compile options
  - compile order; default to alphabetical if no order given
  - conversion rules
    - ignore comments and bracketed text
    - handle italics and bolded blocks
    - convert `--` to the em dash
    - collapse whitespace to single space (i.e. allow newlines in paragraphs)
  - conversion options
    - ident paragraphs vs. leave blank line between paragraphs
    - no indent on first paragraph of a section/chapter
  - how to compile
    - text editors can implement this functionality internally
    - alternatively, link to github project with python scripts for compiling

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

Each story written with prose should be placed in its own directory.
The configuration file must be placed in the root directory of the project.
Prose files containing the actual narrative writing can be placed in the
root directory or in subfolders.

Here's a simple example with everything in the project root directory:

```
my-project/
  config.yml
  my-story-chp-1.prose
  my-story-chp-2.prose
  title.prose
```

A more complicated example may look like this:

```
my-project/
  acknowledgements.prose
  appendix.prose
  config.json
  part1/
    chapter-01.prose
    chapter-02.prose
    chapter-03.prose
  part2/
    chapter-04.prose
    chapter-05.prose
    chapter-06.prose
    chapter-07.prose
  part3/
    chapter-08.prose
  title.prose
```

See the section on configuring compilation options for information on
how to order files when compiling a document from prose files.

### Version control

It is highly recommended that all prose projects be placed under
version control. The prose syntax project uses [git](https://git-scm.com/),
but any alternative version control system can be used as well.
Commits should be performed frequently while writing.

At the minimum, this provides psychological safety for a writer. New
portions of the story can be added, rewritten, or deleted without fear
of losing any work. Old version can always be retrieved from the
repository history.

> TODO more advanced usage; collaboration between author and editor;
  using review tools like gerrit

### Best practices

> TODO
  - editor should soft wrap lines
    - line breaks inside a paragraph make it harder when editing
  - use only one blank line after every paragraph
  - enable spell-checking in your editor

### Acknowledgements

- [Fountain](https://fountain.io/)
- [GitHub Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
