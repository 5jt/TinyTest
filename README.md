TinyTest
========

A minimal testing framework for Dyalog APL, consisting of two operators and a function.

-   `match` checks the result of a function is as expected
-   `catch` checks a function signals an error as expected
-   `report` prints how many errors were found

Example test script
-------------------

This test script would be part of another namespace.

```apl
 {ec}←tests;DEBUG;default;dictionary;T
⍝ test the `text` function
⍝ report errors in the session
⍝ and return the number of errors found
 T←##.tinytest ⍝ dependency
 ec←0 ⍝ error count

⍝ ERROR HANDLING
⍝ ==============

  DEBUG←1 ⍝ ON
⍝ ------------

 ec+←(text T.catch 123 'no dictionary')'foo'

 dictionary←0
 ec+←(text T.catch 123 'invalid dictionary')'foo'

  DEBUG←0 ⍝ OFF
⍝ -------------
 ⍝ text should ignore errors and return its right argument

 ec+←(text T.match'foo')'foo' ⍝ no dictionary

 dictionary←0 0 0
 ec+←(text T.match'foo')'foo' ⍝ invalid dictionary

 dictionary←testDictionary
 ec+←(text T.match'foo')'foo' ⍝ no default language

⍝ DYADIC
⍝ ======
⍝ without default
 ec+←'fr'(text T.match'vache')'cow'
 ec+←'fr'(text T.match'foo')'foo'

⍝ with default
 default←'fr'
 ec+←'de'(text T.match'Kuh')'cow'
 ec+←'fr'(text T.match'foo')'foo'

⍝ MONADIC
⍝ =======
 ec+←(text T.match'vache')'cow'
 ec+←(text T.match'foo')'foo'

 ⎕←report ec
```
