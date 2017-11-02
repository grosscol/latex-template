# Latex Template for Kindle

Shamelessly copied from (http://todd-davies.github.io/2014/01/08/latex-and-the-kindle/)

tl;dr
-------------

I've got a [project](https://github.com/Todd-Davies/latex-template) on Github
that makes it easy to produce multiple `pdf` files with different styles but the
same content. Handy for producing documents for the multiple formats.

---------------------------------------

Just before Christmas I bought a Kindle, the main justification being that I
could use it to read my university course notes on there rather than printing
them all off and wasting reams of paper.

The problem
-------------

I use [LaTeX](http://en.wikipedia.org/wiki/LaTeX) to produce my notes as `.pdf`
files, that up to now, have been formatted as A4 sized documents. However, if
you've ever tried to view a pdf file on a
[kindle](http://www.amazon.co.uk/gp/product/B007HCCOD0/ref=ksfs_sz) (I've got
the basic model), then you'll know that it maps each page of the pdf file on to
the screen without any scaling. Ah.

This is an understandable decision on Amazon's part; the pdf format was created
to be like 'digital paper', and so it might not be wise (or even feesable) to
just reformat the file so that it fits nicely on the screen of the kindle.
Uunfortunately, this results in the page being squashed down to less than half
it's original size, resulting in minute, even unreadable text. The kindle does
offer zoom functionality, but it's a pain to use, and ruins the experience.

The solution was to set up my project so that two pdf files would be created
when I compiled my notes file; one would be A4 formatted, and the other sized to
fit a kindle screen.

<!--more-->

The solution
-------------

I decided that the easiest and most logical way to produce two output pdf files
was to split my LaTeX source file into multiple parts:
 - `content.tex` - holds the actual content of the notes.
 - `packages.tex` - holds the LaTeX packages required by the content file.
 - `meta.tex` - holds information such as the name of the author and the title of the file.
 - `notes.tex` - contains the style information for formatted A4 notes
 - `kindle.tex` - contains the style information for kindle formatted notes.

I then have a bash script that I run in order to compile the project and
generate the pdf files:

{% highlight bash linenos=table %}
#!/bin/bash
aspell -t check content.tex
aspell -t check meta.tex
pdflatex notes.tex
pdflatex kindle.tex
{% endhighlight %}

When I run `build.sh`, the content files get spell checked and then both the
notes and kindle files get compiled to produce `notes.pdf` and `kindle.pdf`.
