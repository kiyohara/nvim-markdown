# Nvim Markdown

Fork of [vim-markdown](https://github.com/plasticboy/vim-markdown) with extra mappings.

## Installation

This plugin requires Neovim 0.5+

Use a package manager like [vim-plug](https://github.com/junegunn/vim-plug) to install it.

To install with vim-plug add: `Plug 'ixru/nvim-markdown'`

To install manually instead, see `:help plugin`

## Features

* Syntax highlighting with concealment of links and text formatting.
* Fold headers and lists by pressing `tab` in normal mode.
* Insert checkboxes `[X]` by pressing `Control-c` in insert or normal mode.
* Auto-inserts bullets on newline; can be removed again with `backspace` while preserving indentation, or `tab` to create a sub-list.
* Create links `[link text](url)` by pressing `Control-k` in normal or insert mode. If pressed over an url, or in a word, it will autofill the correct field. 
 `tab` can be used in insert mode to skip from one field to the next.
* Follow links with `Return`. Works with both `[[link text]]` file links and `[link text](url)` style links.
  If the url is not an http address it will be treated like a file link.

### Concealing

Concealing is set for some syntax such as bold, italic, code block and link.

Concealing lets you conceal text with other text. The actual source text is not modified. If you put your cursor on the concealed line, the conceal goes away.

[Options](#options) are available to disable or change concealing.

Try `:help concealcursor` and `:help conceallevel` for details.

## Options
<details><summary>Enable TOC window auto-fit</summary>

Allow for the TOC window to auto-fit when it's possible for it to shrink.
It never increases its default size (half screen), it only shrinks.

        let g:vim_markdown_toc_autofit = 1
</details>


<details><summary>Text emphasis restriction to single-lines</summary>

By default text emphasis works across multiple lines until a closing token is found. However, it's possible to restrict text emphasis to a single line (i.e., for it to be applied a closing token must be found on the same line). To do so:

        let g:vim_markdown_emphasis_multiline = 0
</details>

<details><summary>Syntax Concealing</summary>

Concealing is set for some syntax.

For example, conceal `[link text](link url)` as just `link text`.
Also, `_italic_` and `*italic*` will conceal to just _italic_.
Similarly `__bold__`, `**bold**`, `___italic bold___`, and `***italic bold***`
will conceal to just __bold__, **bold**, ___italic bold___, and ***italic bold*** respectively.

To enable conceal use Vim's standard conceal configuration.

        set conceallevel=2

To disable conceal regardless of `conceallevel` setting, add the following to your `.vimrc`:

        let g:vim_markdown_conceal = 0

To disable math conceal with LaTeX math syntax enabled, add the following to your `.vimrc`:

        let g:tex_conceal = ""
        let g:vim_markdown_math = 1

</details>

<details><summary>Fenced code block languages</summary> 

You can use filetype name as fenced code block languages for syntax highlighting.
If you want to use different name from filetype, you can add it in your `.vimrc` like so:

        let g:vim_markdown_fenced_languages = ['csharp=cs']

This will cause the following to be highlighted using the `cs` filetype syntax.

    ```csharp
    ...
    ```

Default is `['c++=cpp', 'viml=vim', 'bash=sh', 'ini=dosini']`.
</details>

### Syntax extensions

The following options control which syntax extensions will be turned on. They are off by default.

<details><summary>LaTeX math</summary>

Used as `$x^2$`, `$$x^2$$`, escapable as `\$x\$` and `\$\$x\$\$`.

    let g:vim_markdown_math = 1
</details>

<details><summary>YAML Front Matter</summary>

Highlight YAML front matter as used by Jekyll or [Hugo](https://gohugo.io/content/front-matter/).

    let g:vim_markdown_frontmatter = 1
</details>

<details><summary>TOML Front Matter</summary>

Highlight TOML front matter as used by [Hugo](https://gohugo.io/content/front-matter/).

TOML syntax highlight requires [vim-toml](https://github.com/cespare/vim-toml).

    let g:vim_markdown_toml_frontmatter = 1
</details>

<details><summary>JSON Front Matter</summary>

Highlight JSON front matter as used by [Hugo](https://gohugo.io/content/front-matter/).

JSON syntax highlight requires [vim-json](https://github.com/elzr/vim-json).

    let g:vim_markdown_json_frontmatter = 1
</details>

## Mappings

The following work on normal and visual modes:

-   `]]`: go to next header. `<Plug>Markdown_MoveToNextHeader`
-   `[[`: go to previous header. Contrast with `]c`. `<Plug>Markdown_MoveToPreviousHeader`
-   `][`: go to next sibling header if any. `<Plug>Markdown_MoveToNextSiblingHeader`
-   `[]`: go to previous sibling header if any. `<Plug>Markdown_MoveToPreviousSiblingHeader`
-   `]c`: go to Current header. `<Plug>Markdown_MoveToCurHeader`
-   `]u`: go to parent header (Up). `<Plug>Markdown_MoveToParentHeader`

This plugin follows the recommended Vim plugin mapping interface, so to change the map `]u` to `asdf`, add to your `.vimrc`:

    map asdf <Plug>Markdown_MoveToParentHeader

To disable a map use:

    map <Plug> <Plug>Markdown_MoveToParentHeader

## Commands

The following requires `:filetype plugin on`.

- `:HeaderDecrease`: Decrease level of all headers in buffer: `h2` to `h1`, `h3` to `h2`, etc.
 
  If range is given, only operate in the range.
  If an `h1` would be decreased, abort.
  For simplicity of implementation, Setex headers are converted to Atx.
- `:HeaderIncrease`: Analogous to `:HeaderDecrease`, but increase levels instead.
- `:SetexToAtx`: Convert all Setex style headers in buffer to Atx.
 
  If a range is given, e.g. hit `:` from visual mode, only operate on the range. 
- `:Toc`: create a quickfix vertical window navigable table of contents with the headers.
  Hit `<Enter>` on a line to jump to the corresponding line of the markdown file.
- `:Toch`: Same as `:Toc` but in an horizontal window.
- `:Toct`: Same as `:Toc` but in a new tab.
- `:Tocv`: Same as `:Toc` for symmetry with `:Toch` and `:Tocv`.
- `:InsertToc`: Insert table of contents at the current line.

  An optional argument can be used to specify how many levels of headers to display in the table of content, e.g., to display up to and including `h3`, use `:InsertToc 3`.

-   `:InsertNToc`: Same as `:InsertToc`, but the format of `h2` headers in the table of contents is a numbered list, rather than a bulleted list.

## Credits

The main contributors of vim-markdown are:

- **Ben Williams** (A.K.A. **plasticboy**). The original developer of vim-markdown. [Homepage](http://plasticboy.com/).

If you feel that your name should be on this list, please make a pull request listing your contributions.

## License

The MIT License (MIT)

Copyright (c) 2012 Benjamin D. Williams

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
