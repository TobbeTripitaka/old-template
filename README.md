# Automatically build Latex pdf articles using various journal templates

Minimize the amount of boilerplate code
needed to start writing an article in Latex.

Uses the build tool [SCons](http://www.scons.org/) to automate the
production and compilation of the Latex sources.

## Usage

First, write your manuscript's body in a .tex file ('body.tex' in this
example):

    \begin{abstract}
    Bla bla bla.
    \end{abstract}

    \section{Introduction}
    Many citations using \citet{Author2012}.

    ...
    \section{Acknowledgments}
    Thank you.

Notice that there is no `\begin{document}`, `\bibliography`, `\title`, etc.
All of that is build automatically by the `Manuscript` Python class in
`templates.py`.

After you have your `body.tex` file, copy `SConstruct`, `templates.py`, and
`classes` to your paper's repo. Then, edit `SConstruct` to include the
information about your new paper. It might look something like this:

    import os
    from templates import Manuscript

    env = Environment()
    env.SetDefault(TEXMFHOME=os.path.join(os.environ['HOME'], 'texmf'))
    # To include the class and bibtex files in the 'classes' dir
    env.Replace(TEXINPUTS='classes//:')
    env.Replace(BSTINPUTS='classes//:')

    builder = Manuscript(
        title='My title',
        author=['Me',
                'My friend'],
        affil=['Where we work.',
               'Where only my friend works.'],
        author_affil=[[0], [0, 1]],
        journal='geophysics', # The journal name
        heads=['Me and Friend', 'Short title'],
        bibfile='references.bib')
    # Make the manuscript for submission
    ms = env.Command('manuscript.tex', 'body.tex', builder.build_ms)
    mspdf = env.PDF(target='manuscript.pdf', source=ms)

The `Manuscript` class takes the information about your paper and will produce
`manuscript.tex`. This file will use the document class and the Latex template
for the specified journal (in this case,
[Geophysics](http://library.seg.org/journal/gpysa7)).
The `author_affil` field specifies which affiliations are associated with each
author. `0` means the first affiliation listed in `affil`, `1` the second, etc.

At the moment available templates are:

* `geophysics`: [Geophysics](http://library.seg.org/journal/gpysa7).
* `gji`: [Geophysical Journal International](http://gji.oxfordjournals.org/)

SCons will take care of producing the Latex file and then compiling it to PDf.
To produce the files, run:

    scons

To clean up the directory of the generated files:

    scons -c

The `Manuscript` class also has options to build a pretty version of the
manuscript. Simply add these lines to your `SConstruct` and SCons will produce
both the version for submission and the pretty version:

    # Make a pretty version of the paper
    paper = env.Command('paper.tex', 'body.tex', builder.build_paper)
    paperpdf = env.PDF(target='paper.pdf', source=paper)

## Dependencies

You'll need a Latex distribution and also SCons.

On **Ubuntu Linux** you can install these by:

* using `apt-get`: `sudo apt-get install texlive-full scons`
* alternatively install SCons using `pip`: `pip install --egg scons`

On **Windows**:

* [MikTex](http://miktex.org/) is a popular Latex distribution
* You can download SCons from [their official site](http://www.scons.org/).
* You might also need [Python](http://www.python.org/) in order to make SCons
  work. A nice way to install Python is through the
  [Anaconda distribution](https://store.continuum.io/cshop/anaconda/)
