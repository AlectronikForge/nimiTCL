# nimiTCL - A minimal TCL interpreter in [Nim](nim-lang.org/)

## What?

A toy interpreter in less than *300* loc (current count (incl. empty lines):
**274**).

The original goalpost was *500* loc, but it was in C. Nim aims to be close to C
in terms of speed, but it competes with languages like Python in terms of
expressivity, so I decided to try to make it in under 300. Initial version was
closer to 350 loc, but fortunately I managed to reduce the count without
compromising readability too much.

It's a toy: it doesn't implement the full TCL language and it was never meant
to. That being said, it's easy to extend and if you're willing to go above the
300 loc mark you can quickly make it useful. For this you would need at least:

* better proc implementation (proper call frames)
* expr command
* loops, break and continue
* uplevel and friends

See 'src/main.nim' for supported language constructs.

## How?

Nim is a statically typed, natively compiled (via C) language with rich type
system, a lot of goodies in its standard library, and advanced meta-programming
capabilities. The features I used to make the implementation shorter (compared
to C) include:

* [built-in string](https://nim-lang.org/docs/manual.html#types-string-type)
  type, which is similar to std::string in C++ (all over the place)
* [built-in seq](https://nim-lang.org/docs/manual.html#types-array-and-sequence-types)
  type, which is similar to std::vector in C++ (all over the place)
* [hash tables](https://nim-lang.org/docs/tables.html) provided in stdlib, which
  are like std::map in C++ (for variables and commands lookup)
* [built-in closures](https://nim-lang.org/docs/manual.html#procedures-closures)
  support (for user-defined commands)
* [built-in templates](https://nim-lang.org/docs/manual.html#templates), which
  are like [syntax-rule macros](http://www.willdonnelly.net/blog/scheme-syntax-rules/)
  in Scheme (to simplify defining commands)


## Why?

For fun, mostly. But also to showcase Nim's usefulness.

I started writing this after I read about two other TCL
implementations, done in C, which are around 500 loc:

* [antirez implementation - Picol](http://oldblog.antirez.com/post/picol.html)
* [zserge implementation - ParTcl](http://zserge.com/blog/tcl-interpreter.html)

I never used TCL, what little I know about it comes from
[this article](http://antirez.com/articoli/tclmisunderstood.html) by
antirez. I read it years ago and I rememer I thought that TCL was a
very elegant language - one that combines a few simple concepts into
a strong whole. I later learned about
[fexprs](https://en.wikipedia.org/wiki/Fexpr), the
[vau](http://lambda-the-ultimate.org/node/4093) and
[Kernel language](http://lambda-the-ultimate.org/node/1680), as well as
[PicoLisp](http://picolisp.com/wiki/?home) and [Io](iolanguage.org/) which all
work in a similar way. Still, when learning these, I thought: "Wow, just like
TCL!" - which helped me in their understanding. For that, I'm grateful to
antirez and TCL.