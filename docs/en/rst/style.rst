:orphan:

==============================
Writing Bugzilla Documentation
==============================

The Bugzilla documentation uses
`reStructured Text (reST) <http://docutils.sourceforge.net/rst.html>`_,
as extended by our documentation compilation tool,
`Sphinx <http://sphinx-doc.org/>`_. This document is a reST document for
demonstration purposes. When you build the docs, it gets built (at least in
the HTML version) as a standalone file, although it isn't as readable in that
form because some of the directives discussed are invisible or change when
rendered.

`The Sphinx documentation <http://sphinx-doc.org/latest/rest.html>`_
gives a good introduction to reST and the Sphinx-specific extensions. Reading
that one immediately-linked page should be enough to get started. Later, the
`inline markup section <http://sphinx-doc.org/latest/markup/inline.html>`_
is worth a read.

Bugzilla's particular documentation conventions are as follows.

Block Directives
################

Every heading should be preceded by an anchor, with a globally-unique name
with no spaces. Then we demonstrate the available heading levels we haven't
used yet:

.. _uniqueanchorname:

Third Level Heading
===================

Fourth Level Heading
--------------------

Fifth Level Heading
~~~~~~~~~~~~~~~~~~~

(Although try not to use headings as deep as the 5th level.)

Make links to anchors like this: :ref:`uniqueanchorname`. It'll pick up the
following heading name automatically and use it as the link text. Don't use
standard reST internal links like `uniqueanchorname`_ - they don't work
across files.

Comments are done like this:

.. This is a comment. It can go on to multiple lines. Follow-on lines need to
   be indented.

Other block types:

.. note:: This is just a note, for your information. Like all double-dot
   blocks, follow-on lines need to be indented.

.. warning:: This is a warning of a potential serious problem you should be
   aware of.

Use both of the above block types sparingly. Consider putting the information
in the main text, omitting it, or (if long) placing it in a subsidiary file.

Code gets highlighted using Pygments. Choose the highlighter at the top of
each file using:

.. highlight:: console

You can change the highlighter for a particular block by introducing it like
this:

.. code-block:: perl

  # This is some Perl code
  print "Hello";

There is a
`list of all available lexer names <http://pygments.org/docs/lexers/>`_
available. We currently use ``console``, ``perl``, and ``sql``. ``none`` is
also a valid value.

Inline Directives
#################

.. warning:: Remember that reST does not support nested inline markup. So you
   can't have a substitution inside a link, or bold inside italics.

A filename or a path to a filename is displayed like this:
:file:`/path/to/filename.ext`

A command to type in the shell is displayed like this:
:command:`command --arguments`

We place static values for substitution (using |subst-name|) in the file
:file:`$BUGZILLA_HOME/docs/definitions.rst.tmpl`.
This gets built into definitions.rst, with the script adding some definitions
for minimum module versions etc. generated from the source itself. Lines in
that file look like this:

.. |subst-name| replace:: Some Text Here
