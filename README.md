Guile Interface for Mathematica
===============================

This is a simple library for evaluating an expression in Mathematica.
It defines one procedure `mathematica-eval` which accepts a string,
evaluates it and produc.  It currently doesn't return anything.  I use
it for producing graphs.

Requirements
------------

* GNU Guile Scheme 
* Mathematica

Usage
-----

    $ guile -c '(use-modules (mathematica)) (mathematica-eval "1 + 1")'
    2

TODO
====

* Make it return the resulting expression as a string.

