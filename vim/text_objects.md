## Text Objects
In trying to figure out how to copy a string of text, I came across text objects.

`yi'` copies everything in between single quotes

`ya'` copies everything in between the single quotes AND the quotes

The `i'` and the `a'` are the text objects, defined by the single quotes.  The `i` and the `a` determines if you are only applying the action to the inner text object, or the whole thing.

Other text objects that can be combined with actions:
  - `iw` or `aw` for words
  - `is` or `as` for sentences
  -  `ip` or `ap` for paragraphs
  -  `i(` or `a(` for parenthesized blocks
  -  `i{` or `a{` for brace blocks
  -  `it` or `at` for tag blocks
  -  `ir` or `ar` for ruby blocks

Resources:
  - [Vim Text Objects: The Definitive Guide](http://blog.carbonfive.com/2011/10/17/vim-text-objects-the-definitive-guide/)
  - [Vim Text Objects: The Definitive Guide](http://blog.carbonfive.com/2011/10/17/vim-text-objects-the-definitive-guide/)
