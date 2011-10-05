ocaml skeleton
==============

`ocaml_skeleton` is a scaffolding framework to get up and running build OCaml
applications quickly. It provides a filesystem structure and _oasis file, which
generates all other components, such as _tags, Makefile, myocamlbuild.ml, etc.

OCaml is relatively difficult to navigate as a new user. While the language has
ample online documentation, the development environment itself can be remarkably
opaque. The problem is compounded by numerous sites providing half-working
snippets of code that range from fresh to very, very old. The only way to
discover 'the modern way of doing things' is through mailing lists or IRC. Since
I hate interacting with humans and know others do as well, I thought it would be
nice to provide a jumpstart environment for someone to get code up-and-running.
An example application with unit tests seems to be a nice sandbox for language
discovery.

*Caveat Emptor*: The system I've provided here works for me but I am still
inexperienced with the language -- especially with respect to the module system
and how ocamlbuild discovers dependencies. If you are more familiar with OCaml
and have input on how larger, more established build systems operate than I
would be grateful for any feedback.

instructions
============

os dependencies
---------------

For debian/ubuntu, running the following should work:

```bash
> sudo apt-get install aptitude` # if you don't have it already

> sudo aptitude install ocaml-base-nox ocaml-nox ocaml-batteries-included
ocaml-findlib ocaml-interp libounit-ocaml-dev oasis
```

Oasis is needed for generation setup.ml/_tags/Makefile/etc. after changing _oasis file.


If you manage to get set up on other OSes (other Linuxen, OSX, BSD) please send
me your strings!

usage
-----

`ocaml setup.ml -configure` to configure project

`ocaml setup.ml -build` to build it

The `Makefile` autogenerated to run commands above.

In short:

```bash
  > ocaml setup.ml -all
```

The source for the application is in `src/main.ml` and any subdirectories.
When you write more your own modules, make sure you add it to _oasis file.
More info about _oasis file and oasis tool can be found at the [oasis user
manual](https://oasis.forge.ocamlcore.org/MANUAL.html).

Dependencies for your files are described in fields BuildDepends in _oasis
file.
To add another dependency simply add it to corresponding field.
Let's say you want to use the
[PCRE](http://www.pcre.org/) package installed with `sudo aptitude install
libpcre-ocaml-dev`. You add `open Pcre;;` in `src/calc/calc.ml`, then add
following line to section `Library calc` in  `_oasis` file:
```
BuildDepends: pcre
```
Tests are written in `tests/tests.ml`. Make sure the `OUnit` package is opened,
open up your module, and write some tests using the
[OUnit](http://ounit.forge.ocamlcore.org/api) framework. For a reference, here
is a list of [available testing
methods](http://ounit.forge.ocamlcore.org/api/OUnit.html).  Note that you must
add your tests to the `suite` for them to run. I tried adding in the code found
at [Skydeck](http://skydeck.com/blog/programming/unit-test-in-ocaml-with-ounit)
but I couldn't make it work nicely with separate testing modules. However,
having the tests hand-added gives you the full flexibility of OUnit.

todo
====

see the GitHub issues page, but:

* instructions for OSX/BSD/other distros
* make tests nicer (separate test files?)
* add optimized builds
* make ocamlbuild integration less hacky
* automatically make a library


resources
=========

* OCaml style guide: http://www.cs.caltech.edu/~cs20/a/style.html
* Sample OCaml code (cross-referenced with other languages):
  http://pleac.sourceforge.net/pleac_ocaml/
* The default vim plugin for .ml files has an annoying textwidth setting. Try
  this to turn that off: `echo "set tw=0" >> ~/.vim/after/indent/ocaml.vim`

thanks
======

The OCaml community has a lot of high quality software written by high quality
people. It's my hope that providing this starter kit will lure in many more.

If you'd like to contribute, branch off next and send a pull req.
