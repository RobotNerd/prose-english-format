# Prose Syntax - English

The Prose syntax for the English language is a way to bring aspects of
programming to the written word. It introduces syntax highlighting
and functionality to help writers visualize their stories and catch
some common mistakes early.

If you write in another language, please take the ideas here and
adapt them to your language of choice! Related projects will be included
here.

> TODO plugins that implement prose-syntax-english

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

### Metadata

> TODO
  - title
  - author
  - section
  - chapter
  - section breaks

### Comments

> TODO
  - line comment
  - block comment

### Brackets

Special notes are placed inside a pair of brackets `[]`.

> TODO

### Tags (TODO, FIXME, etc.)

> TODO

### Special names

> TODO
  - when available, prose editor plugins should automatically and
    temporarily add everything in the .names file to the dictionary
    for the editor. The purpose is to ensure that the spell-checker
    recognizes these words.
  - refer to folder structure section regarding location of .names file

### Syntax highlighting

> TODO

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
