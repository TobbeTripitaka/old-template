# Templates for articles and expanded abstracts

Use these templates to start writing.

Templates usually contain:

* A `Makefile` with rules to build your manuscript, count words, clean the
  directory.
* A manuscript template in either Latex or Pandoc Markdown (`manuscript.tex` or
  'manuscript.md`.
* A sample Bibtex reference file.
* The Latex classes and bibliography style files you'll need for that
  particular journal.

## Software

Most of this is meant to work on GNU/Linux but might work on Windows as well.

On **Linux** you'll need:

* Latex: the usual Latex distribution in Debian/Ubuntu is `texlive`. I
  recommend installing the `texlive-full` package
  (`sudo apt-get install texlive-full`).
* Pandoc: follow the instruction on
  [the official site](http://johnmacfarlane.net/pandoc/)

On **Windows** you'll need everything above and also:

* MinGW: to get `make`.

For extra points, you can install [msysgit](http://msysgit.github.io/) to also
get a bash shell.
