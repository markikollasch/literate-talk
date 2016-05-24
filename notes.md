# What is literate programming?

Literate programming is embedding a program's source code into a document describing the program.
This is distinguished docstrings, in which a document describing a program is embedded into the program's source code.
However, literate programs are like docstrings in that the document renderer and the compiler both accept the same artifact as input.
The important difference is that docstrings must conform to the structure required by the computer,
whereas the _natural language_ of a literate program can be organized into a _natural structure_.

> Instead of imagining that our main task is to instruct a _computer_ what to do,
> let us concentrate rather on explaining to _human beings_ what we want a computer to do.
>
<cite>Donald Knuth</cite>

# How does it work?

At its most basic, as implemented in systems like `web`, `cweb`, `noweb`, `Literate`, etc.,
the programmer interleaves marked-up natural language text and arbitrary blocks of source code.
The source code blocks are named, effectively defining macros which expand to the enclosed code.
Elsewhere in the text are macro invocations.

Using the `weave` operation, the text and source code are formatted and the macro invocations elided,
producing a human-readable document text document with excerpts of "out of order" source code.

Using the `tangle` operation, the text is elided, and all macro invocations are expanded fully,
producing machine-readable source code in the correct order.

# What's the benefit?

Because the definition and invocation of each macro is independent,
the document can be written in the order that makes rhetorical sense.
It is not required to conform to the logical structure of the source code.
That, in turn, means the author can present a broader context for the program,
and can draw the reader's attention to arbitrary constructions.

A docstring, by contrast, can only describe certain semantically complete code structures individually.
Whereas a docstring is strictly useful for producing reference material,
a literate program has far more pedagogical versatility.

Additionally, literate programming as a discipline can have other advantages.
The purpose of the exercise is to produce both a program and a document explaining it.
That means two things:
first, because the programmer explains the code, she must at least attempt to make the code explainable;
second, because the documentation and the program originate from the same source,
there is less opportunity for the documentation to drift into inaccuracy.
Since the documentation is emphasized even over the program itself,
optimstically, the programmer will be less inclined to neglect it.
This is in addition to incurring all of the benefits of the existence of documentation.

# What's the cost?

Literate programming requires the programmer also to be an essayist.
It lengthens the build process by one step,
in which the programmer has abundant new opportunities to commit a syntactic error.
The tool so added may integrate poorly with the rest of the toolchain.

In agile programming methodologies, documentation of source code is often specifically omitted,
on the grounds that updating both code _and_ documentation to reflect changed requirements
is more expensive and error-prone than simply updating the code;
that it disincentivizes the writing of code whose quality is so high as to be self-describing;
that a document which drifts into inaccuracy is more harmful than the absence of a document;
and that the code as well as the program should be simple enough to need no documentation.
Practicing literate programming may be at odds with these virtues.

Additionally, for some code, documentation just isn't that valuable.

# But --

Recall that literate programming is the embedding of a program's code within a document describing the program.
Most teams _already have_ a document describing their program: the issue tracker.
It's a highly specialized hypertext document requiring a highly specialized reader,
but it's a document nevertheless.
It's a description of the fulfilled and known unfulfilled requirements of the program,
often together with the context in which those requirements were determined.
It is presented alongside a formalized practice to mitigate the harm of drift:
once an issue is closed, it hardly matters if requirements subsequently change.

A given issue has only very weak cohesion with the code that closed it.
To travel from issue to code, assuming all conventions have been observed,
one checks the issue for annotations containing a revision number
(or cross-references commit messages containing issue numbers),
then reviews the code changed in that commit.
To go from code to an issue is worse:
one uses a "blame" tool to find the revision that introduced behavior,
then checks the commit message for the issue number.
When considering a requirement, two important questions are
"How was this fulfilled?" and "What demonstrates that this was fulfilled?"
The answer is found in the code: implementation and tests respectively.
When considering code, an important question is "What is this for?"
The answer is found in the issue that formalized the requirement.

What's more, oftentimes the issue tracker and the version control system are separate,
so that it's easy to have access to only one of the code and the issues.

# We can do better

All of the above problems can be alleviated considerably by robust tooling.
Github alone significantly reduces this friction by automatically cross-referencing issues mentioned in commit messages,
and by hosting an issue tracker
(and a wiki, for non-literate documentation)
alongisde the repository.

An expansion of literate programming suggests a means to improve this, however.
If the entire codebase is literately embedded into the issue tracker,
and the issue tracker is committed to version control,
then the repository will be a _human-readable_ description of its own rationale.

One can imagine the workflow:
A PM formalizes a requirement by creating an issue file and committing it to the repository.
A developer annotates that requirement file with a macro whose body is a test of that requirement,
then invokes that macro from wherever the test runner requires tests to be written.
The implementation of the required behavior can also be embedded directly alongside the issue,
or somewhere else that makes rhetorical sense.

# Some other things I want to mention

[Racket](http://racket-lang.org/)'s literate programming tool,
[`lp2`](https://docs.racket-lang.org/scribble/lp.html)
is built on Scribble, Racket's documentation tool.
Scribble is both a library for rendering hypertext and an alternate syntax,
effectively resulting in a markup language that is semantically identical to,
and fully interoperable with, Racket.
With `lp2`, a literate program can be `require`d just like a normal Racket module,
and documentation rendered just like a normal Scribble file,
without any preprocessing step or source mapping, and it can be debugged etc. with the same tools as the code.

This makes Racket well-suited as a platform for an exploration of this concept.
