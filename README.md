EngCel
======

Engineering extensions for Microsoft Excel

EngCel is an add-in that will ultimately provide extened functionality to make Excel more suitable for Engineering Calculations.

Currently Excel 2003 - 2010 is supported, however it is likely to be compatable with older/newer versions.

A semi-comprehensive illustrated introdction can be found at:
* [In-line super/sub script in Excel and More - Being Brunel](http://www.beingbrunel.com/inline-subsuper-script-in-excel-and-more/ "Being Brunel")


Installation
------------

EngCel is a VBA add-in, which means it can be installed from Excel. This can be done for a single session just by opening the file, or permenantly by loading the EngCel.xla file.

The method for loading add-ins varies between versions of Excel:

* [Loading an add-in for Excel 2007 and 2010](http://office.microsoft.com/en-us/excel-help/load-or-unload-add-in-programs-HP010096834.aspx#BMexceladdin "Excel 2007 to 2010")
* [Loading an add-in for Excel 2003](http://office.microsoft.com/en-us/excel-help/load-or-unload-add-in-programs-HP005203732.aspx "Excel 2003")


Usage
=====

When loaded EngCel provides the following extensions:

In-line Engineering Notation
----------------------------

The Pipe Parser extension loads automatically with the EngCel. This provides a simple mark-up language, based on LaTeX, which allows super/sub script notation and Greek symbols to be typed directly into the formula bar.

To use the parser start a cell with a pipe "|" this indicates that the text in the cell should be processed using the following rules:

* ^ - The next charactor should be in super-script
* _ - The next charactor should be in sub-script
* ¬ - The preceeding charactor should have a bar over it
* {} - Mark-up between brackets should be considered as a single charactor
* \Alpha - Insert the Greek symbol stated, where proper case denotes a capatal, and lower case a little letter. There are also a number of mathematical symbols available, however I haven't had the chance to define these just yet- just give it a go!
* \ - The next charactor should be escaped if it is a special charactor
* @ - Inserts 'mixin' codes, see below

For example:

```
|kN/mm^2
```

Would become kN/mm²

Although why you'd want to write that, I'm really not sure!

Mixin codes are available, by piping the name of the mixin the cell will be replaced with a templated cell. At the moment mixins can only be harcoded into EngCel, however alternatives are being investigated. The following mixins are known:

* @pass - A 'Pass' or 'Fail', green/red conditionally formated cell referencing the utilisation percentage two left from the cell. To reverse the sense use @!pass.
* @ok - A 'OK' or 'Check', green/red conditionally formated cell referencing the utilisation percentage two left from the cell. To reverse the sense use @!ok.
* @eng - Format cell to shown engineering exponent notation (i.e. x10^3, ^6, ^-3), etc.
* @colour - Switch on and off function colouring, see below for more information.
* @help - Create a new sheet with this help file and an charactor map


Function Colouring
------------------

To enabled EngCel will enable mod_colour. This modification to Excel will colour functions depending on their relationships:

* Formulas that are neither used by, or use other cells will turn gray (unused value)
* Formulas that are used, but not used by, other cells will turn red (input value)
* Formulas that only reference a single cell, without calculation, will turn orange (refered value)
* Formulas that rely and are relied upon by other cells will turn blue (function)
* Formulas that use other cells but are not used themselves will turn green (result value)

Because of limitations in Excel, mod_colour disables the undo function, and therefore is now switched on when Excel starts.

To enable mod_colour, use the mixin |@colour. This will return either 'on' or 'off' representing the state of mod_colour after the switch. Note that mod_colour will only effect cells altered when it is on.


Author and Licence
==================

Challenger is primiarly written by Thomas Michael Wallace (www.thomasmichaelwallace.co.uk), and released under the GPL v3 licence.
