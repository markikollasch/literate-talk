# Literate programming

# Why?

> Instead of imagining that our main task is to instruct a _computer_ what to do,
> let us concentrate rather on explaining to _human beings_ what we want a computer to do.
>
<cite>Donald Knuth</cite>

# What is it?

- Embedding a program's source code into a document describing the program
- A programming paradigm emphasizing extreme readability
- A kind of fancy preprocessor for pretty-printing

# Like docstrings, but...

- Code embedded in documentation instead of vice versa
- Document structure independent of code structure
- Arbitrary pedagogical construct instead of reference material only

<div class="notes">
  "Keeping code and documentation together? Isn't that what a docstring is?"
</div>

# How do you do it?

- Write an essay in natural language with markup
- Write chunks of code wherever it's rhetorically convenient
- Each chunk defines a named macro
- Invoke macros in the structure demanded by the compiler or interpreter
- `weave` the literate source to format the essay
- `tangle` the literate source to emit valid source code

<div class="notes">
  Chunk of code need not have semantic significance.
The source code is only valid if you did it right.
</div>

# History

- _Literate Programming_ by Donald Knuth (1984)
- `WEB` implementation (1984): Pascal program and TeX document
- `CWEB` (1987):  C, C++, and Java; TeX
- `noweb` by Norman Ramsey (1989): first language-agnostic system
- Racket `scribble/lp2` module: Self-hosting Scheme library
- `Literate` (2015): language-agnostic, Markdown-like syntax, source mapping

<div class="notes">
  Source mapping to trace compiler errors back to lines in the literate source, not the emitted code

  Racket version uses Racket itself for everything, including markup. Maybe it's the most promising for study because of its flexibility. Say "Code is Data"
</div>

# What's it good for?

- Extreme readability: human-readable natural-language text is first-class output
- Clear thought: if the programmer explains the code, it must be explainable
- Prevent documentation and code from drifting apart

<div class="notes">
  - Or "she must at least attempt to ensure it's explainable"
  - Many approaches to limiting documentation drift:
    - Agile development often foregoes documentation altogether
    - Python and Rust has executable docstrings that are unit tests
</div>

# What's it not so good for?

- If you don't intend to produce a document, there's no value
- Additional effort to write it
- Less push for "self-documenting" code quality
- Increases toolchain complexity
- Programmer must also be literate

# Is there a place for LP in modern software development?

<div class="notes">
DON'T ADVANCE YET.
There is a document closely related to the source code: the issue tracker.
It's a highly specialized document requiring special software to read and write, but it's a document.
It describes the codebase's past, present, and future, with a specific emphasis on the requirements and the rationale.
Embed test cases and implementation directly within the story.
Commit the whole thing to the repository.
</div>

# Literate issue tracking?

- Issue tracker is a document
- Embed test case in story instead of cross-referencing through revision numbers

# Questions?
