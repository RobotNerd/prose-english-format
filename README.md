# Prose Syntax - English

The Prose syntax for the English language is a way to bring aspects of
programming to the process of writing literature. The main feature of is
syntax highlighting, which helps writers visualize the grammatical structure
of the text. The goal is to quickly catch some common mistakes made by
writers while writing.

If you write in another language, please take the ideas here and
adapt them to your language of choice! Related projects will be included
here.

> TODO plugins that implement prose-syntax-english

> TODO
  - add notes a/b the intended usage; use LaTeX if you need something fancy

### File extension

Prose files are text-only and use the file extension `.prose`.

### Grammar

Prose documents are structured as a series of paragraphs. The rules
below describe how prose expects the writing to be structured.

- Paragraphs are separated by at least one blank line.
  - Multiple contiguous blank lines are allowed.
  - Lines that contain only whitespace characters are treated as blank lines.
- Paragraphs are left-justified, i.e. no whitespace at the
  beginning of the line.
  - Any proceeding whitespace on a line turns a paragraph into a block quote.
  - All lines of a block quote should be indented by the same amount
    of whitespace. However, if there is not a blank line separating multiple
    indented lines, those lines will be considered part of the same paragraph.
    In this case, the indentation level of the first line of the paragraph
    defines the indentation of the block quote.
  - Multiple levels of embedded block quotes are allowed.
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
  by two contiguous hyphens `--` within a paragraph.

### Structural markup

Special markup tags can be used to define document structure.

General rules:
- Tags must be left-justified.
- A tag must be on its own line.
- Multiple tags can be grouped together on contiguous lines,
  but they should be separated from paragraphs by a blank line.

> TODO Consider allowing multiple titles per project. For example,
       an anthology of short stories would have a title and author
       for each story. Be smart enough to treat the title tag the
       same as a chapter in this scenario.

Structural tags:
- Title
  - The tag `Title:` followed by the title of the work.
  - There can be only one title per project.
  - The title should be in the very first document in the .compile
    file (see [Configuration: project compilation options](#configuration-project-compilation-options)).
  - The title should be on the first line of the file in which it is located.
  - All text between the `Title:` tag and a line break is recognized
    as the title of the project.
- Chapter
  - The tag `Chapter:` acts the same as `Title:` unless otherwise noted.
  - There can be multiple chapter tags per project.
  - All text between the `Chapter:` tag and a line break is recognized
    as the title of the project.
    - Adding a chapter title is optional. In other words, a line with
      only the text `Chapter:` will act as a chapter break.
- Author
  - The tag `Author:` must be followed by the name of the writer.
  - Author tags can be placed immediately after title, chapter, or section tags.
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

Line comments:
- Begin with `##`.
- End at the next line break.
- There must be whitespace before the `##` unless it is at the
  beginning of the line.
- Adding a backslash as a prefix `\##` will prevent the double hash from
  being recognized as a comment.

Block comments:
- Begin with `###` and end at the next `###` (or at the end of the file).
- Whitespace must occur before the opening `###` unless it is at the
  beginning of the line.
- Everything between the opening and closing comment tags is considered
  part of the comment. If no matching `###` is found, the comment block
  extends to the end of the file.
- Adding a backslash as a prefix `\###` will prevent the triple hash from
  being recognized as the beginning or ending of a block comment.

### Brackets

Special notes are placed inside a pair of brackets `[]`. When converting
to other formats, the bracketed block of text is ignored.

- Begin with a `[`.
- End at `]` or the end of the file if no closing bracket is found.
- Adding a backslash as a prefix will prevent the opening/closing bracket
  from being recognized as a bracketed block.

### Comment tokens

Comment tokens are capitalized words that provide special metadata for
an author or editor. They are recognized when placed in comments
or bracketed blocks.

These tokens are recognized:
- FIXME
- IMPORTANT
- NOTE
- TODO

### Configuration file

Each prose project can optionally include a configuration file specific to
that project. It is located in the project root (see
[Folder structure](#folder-structure)). The following formats are supported:
- json
- yaml

The configuration file is named `config.*` with the appropriate file
extension based on the file format (e.g. `config.json` or `config.yml`).
Text editors and conversion tools that support prose should attempt to
autodetect the file format when possible, regardless of file extension.

The configuration file can contain:
- project compilation options
- special names used in the project

Available configuration options are detailed in the subsections below.

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
- Name patterns
  - Name patterns are added as a list of values under the appropriate section.
  - Each name pattern is treated as a regular expression.
  - A name pattern is matched with text in a prose document as long as that
    portion of the text is not adjacent to any of these characters:
    - A-Z
    - a-z
    - 0-9
    - \_
    - Example:
      - pattern: Chuck
      - two matches: She looked at Chuck and said, "Hey Chuck!"
      - no matches: He chucked it over the fence and yelled, "Chucks!"
- Spell checking
  - When possible, name patterns should temporarily be added to
    the dictionary of the text editor. This is to ensure that these
    names are not shown as misspellings by built-in spell checkers.
    This is useful, for example, for invented names in fictional stories.
  - Spell checking of these patterns should only occur for prose
    files in the same project as the configuration file from which the
    name patterns were loaded. The names unique to one story should not
    be permanently added to the spelling dictionary so they don't bleed
    over into other projects where those names might not be valid.

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
      "Pleasantville( High School)?",
      "Willow Street"
    ],
    "things": [
      "laser cannon",
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

Prose documents are compiled to other formats for publication. This
section describes the compilation options that can be included in
the configuration file. All of these options are placed in the
configuration file under the `compile` section.

See [Compiling prose](#compiling-prose) for how to compile projects.

##### File order

An optional `order` section can be included to define a specific
order in which prose files are added to the project. This is a list of
file paths relative to the project root. If a file exists in the
project directory but isn't included in the order list, then it will
not be added to the compiled output.

If no `order` field exists in the config file, then all prose files
found in the project and its subfolders will be compiled in alphabetical
order. This order takes into account the full path
from the project root to the file. A subdirectory can be included, and
all files under that subdirectory will be recursively added in
alphabetical order.

Here is an example portion of `config.yml`:

```
---
compile:
  order:
    - title.prose
    - chapter01/
    - chapter02/
    - epilogue.prose
    - acknowledgements.prose
```

##### Conversion options

These conversion rules are used when compiling prose to another
document format. If the document type of the output document does not
support a feature (e.g. bold, italic text), the prose-specific markup
characters are removed but no additional changes are made.

- Comments and bracketed text blocks are ignored.
- The `*` and `__` for italics and bold text are removed, and the text
  between is converted to italics or bold in the output document.
- `--` is converted to the em dash (U+2014) character.
- All empty lines between paragraphs are removed.
- All contiguous whitespace in a paragraph (up until the first completely
  blank line) is collapsed into a single space.
- The first line of a paragraph is indented with a tab.
  - The first line of the first paragraph of a chapter or a section is not
    indented with a tab by default. This behavior is configurable.
  - The title tag and chapter tag are treated the same for this
    feature. This ensures that short stories, which have a title but no
    chapters, will be treated the same.

The following rules are configurable:
- `compile.paragraph.tabFirstParagraph` controls if and when a tab is
  added to the first line of a paragraph. Options are:
  - __never__: (default) Do not use a tab in front of the first paragraph
    in a chapter or story.
  - __always__: Always insert a tab in front of the first paragraph for
    chapters and stories.
  - __chapter__: Insert a tab in front of the first paragraph only for
    chapters.
  - __section__: Insert a tab in front of the first paragraph only for
    sections.
  - Example:
    ```
    ---
    compile:
      paragraph:
        tabFirstParagraph: always
    ```
- `compile.paragraph.removeBlankLines` controls whether blank lines between
  paragraphs are removed.
  - __always__: (default) Remove blank lines between paragraphs.
  - __never__: Leave blank lines to separate paragraphs.
  - Example:
    ```
    ---
    compile:
      paragraph:
        removeBlankLines: never
    ```
- `compile.spacing` controls the line spacing of the output document.
  - __single__: (default) Use single space.
  - __single+__: Use 1.5 spacing.
  - __double__: Use double spacing.
  - Example:
    ```
    compile:
      spacing: single
    ```

> TODO
  - conversion options
    - include "title", "chapter", "section" labels

### Compiling prose

> TODO
  - how to compile
    - text editors can implement this functionality internally
    - alternatively, link to github project with python scripts for compiling
  - target formats
    - (?) ebook formats
    - Microsoft word
    - ods
    - pdf
    - text

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

Here is a simple example with everything in the project root directory:

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

See [Configuration: project compilation options](#configuration-project-compilation-options)
for information on how to order files when compiling a document from
prose files.

### Version control

It is strongly recommended that all prose projects be placed under
version control. The prose syntax project uses [git](https://git-scm.com/),
but any alternative version control system can be used.
Commits should be performed frequently while writing.

At the minimum, this provides psychological safety for a writer. New
portions of the story can be added, rewritten, or deleted without fear
of losing any work. Old version can always be retrieved from the
repository history.

> TODO more advanced usage; collaboration between author and editor;
  using review tools like gerrit

### Best practices

The following are suggested best practices for using prose:
- Text editors should be configured to line wrap.
  - Don't manually add line breaks within a paragraph.
  - Line wrapping makes it much easier to edit text in paragraph form.
- Enable spell checking in the text editor.
- Leave __two__ blank lines after title and chapter structural markup blocks.
  ```
  Title: My Story
  By: Mary Sue


  It was a dark and story night...
  ```
- Leave only __one__ blank line between paragraphs.
- Leave __two__ empty lines above and __two__ empty lines below a
  section break.
  ```
  ...and that's the last I heard from him.


  ---


  That night, we walked down the gravel road under the light of the...
  ```
- Comments
  - Leave __one__ space before the double/triple hash of a comment,
    unless it starts at the beginning of a line.
  - Leave __one__ space after the double/triple hash of a comment, unless
    it is at the end of the line.
  - Leave __one__ space before the opening and closing block comments, unless
    it starts at the beginning of the line.
  - Comment examples:
    ```
    ## This is a comment.
    This text is part of the story. ## And this part is a comment.

    This paragraph ### this comment isn't part of the paragraph ### has an
    embedded block comment.

    ###
    This entire section is commented out.
    ###
    ```
- Brackets vs. comments
  - Use comments to cut out text that you don't want as part of the story
    but aren't ready to delete yet.
  - Use brackets for notes written by the author or editor. In other words,
    these take the place of writing notes in red ink on a printout of
    a story.
- Comment tokens should be added to bracket blocks or comment blocks as needed.
  - When editing, search for comment tokens in prose files to find specific
    areas that still need to be worked on.
  - Suggested use of comment tokens:
    - Use `TODO` for portions of a story that haven't yet been written.
    - Use `FIXME` for problem areas that need to be rewritten.
    - Use `IMPORTANT` to flag areas that the writer must pay attention to
      (e.g. a part of the story that will need to be foreshadowed earlier
      in the story).
    - Use `NOTE` for background or supporting information that the author
      or editor will need when working on the story.
  - Examples
    ```
    ## TODO need to write an action sequence here

    [FIXME The character dialogue here is sloppy.]

    ###
      IMPORTANT This hasn't been setup at all. Need to foreshadow it
      in Act 1.
    ###

    ## NOTE I'm pretty happy with the way this section turned out. :)
    ```

### Acknowledgements

- [Fountain](https://fountain.io/)
- [GitHub Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
