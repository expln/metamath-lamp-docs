```
search-pattern ::= sub-pattern*
sub-pattern ::= ['$'modifiers] MATH-SYMBOL*
modifiers ::= modifier*
modifier := '+' | '!' | 'h' | 'a'
```

Meaning of modifiers:
* `+` - match adjacent symbols
* `!` - exact match
* `a` - match only the assertion of a frame
* `h` - match any hypotheses of a frame

Examples (for set.mm database):

* `( -> )` - this search pattern consists of a single sub-pattern without modifiers.
Moreover, each symbol is a constant. 
It will match any expression having these symbols in the same order allowing intervening symbols.
  
  In order for a frame to match this pattern, it is enough that the assertion part of the frame matches it
  or at least one of the hypotheses (if the frame has hypotheses).
  - Example expressions matching this pattern: `|- ( ph -> ps )`, `|- ( ( x = A ) -> ph )`.
  - Example expressions not matching this pattern: `|- ( x = A ) -> ph`
(this expression is not syntactically valid, 
but it shows symbols `(`, `)`, and `->` in the not matching order).


* `wff -> wff` - similar to the previous one, this pattern consists of constants only. 
But some of the constants are type codes. 
Type codes in the pattern will match any variable of the same type. 
Type codes will also match themselves. For example `wff` will match `wff` and `ph`.
  - Example expressions matching this pattern: `|- ( ph -> ps )`, `|- ( ps -> ( ( x = A ) -> ph ) )`.
  - Example expressions not matching this pattern: `|- ( ( x = A ) -> ph )`
  (this expression includes only one wff variable, whereas the pattern expects two; 
`( x = A )` is a wff but the matching algorithm compares only individual symbols).


* `ph -> ps` - this pattern contains variables. 
Each variable will match a variable of the same type. 
If each variable appears only once in a pattern, then names of variables don't matter.
    - Example expressions matching this pattern: 
`|- ( ph -> ps )`, `|- ( ps -> ps )`, `|- ( th -> ph )`, `|- ( ch -> ( ( x = A ) -> th ) )`.
    - Example expressions not matching this pattern: `|- ( ( x = A ) -> ph )`
      (the same reason as for the previous pattern `wff -> wff`).


* `ph -> ps -> ph` - this pattern contains repeating variables. 
This means that when the first `ph` matches a variable, 
then the second `ph` should match the same variable. But this doesn't work in the opposite direction -
if a pattern contains different variables this doesn't mean they should match different content (see the example below).
    - Example expressions matching this pattern:
`|- ( th -> ( ph -> th ) )`, `|- ( ( ch -> ph ) -> ( ch -> ps ) )`, `|- ( th -> ( th -> th ) )`
(notice that in the last example all variables are same; 
it matches because different variables in a pattern don't require their matching content be different).
    - Example expressions not matching this pattern: `|- ( th -> ( ph -> ch ) )`.


* `$+ ph -> ps` - this pattern uses the modifier `+`. 
It requires the symbols to be adjacent in the matching expression.
    - Example expressions matching this pattern: `|- ( ch -> th )`, `|- ( ch -> ( ps -> th ) )`.
    - Example expressions not matching this pattern: `|- ( ch -> ( ( x = A ) -> th ) )`.


* `$! |- ( ph -> ps )` - this pattern uses the modifier `!`. 
It requires the matching expression to match exactly. 
In other words, the matching expression must be of the same length.
    - Example expressions matching this pattern: `|- ( ch -> th )`, `|- ( th -> th )`.
    - Example expressions not matching this pattern: `|- ( ch -> ( ps -> th ) )`.

* `$a ph -> ps` - this pattern uses the modifier `a`.
It restricts the search engine to check only the assertion part of each frame. 
Hypotheses will not be taking into account when matching.

  
* `$h ph -> ps` - this pattern uses the modifier `h`.
It will match all frames having at least one hypothesis matching the pattern `ph -> ps`.
The assertion part of frames will not be taking into account when matching.
  

* `$a+ ph -> ps` - modifiers can be combined. 
This pattern requires matching symbols to be adjacent 
and only the assertion part of each frame will be checked.


* `$h x = A -> ph <-> ps $a ph -> ph` - this pattern consists of two sub-patterns. 
For a frame to match this pattern it must have at least one hypothesis matching the first sub-pattern,
and its assertion must match the second pattern. 

  The second sub-pattern uses the same variable `ph` twice, 
this means that the second `ph` must match the same content what was matched by the first `ph`.
The first sub-pattern also contains `ph`, 
but it doesn't depend on the `ph` matched by the second sub-pattern. 
Same variables in different sub-patterns are not connected. 
This is a limitation because such algorithm would be difficult to implement.


* `$h+ x = A $h+ x = A $a ph -> ph` - this pattern consists of three sub-patterns.
The first two sub-patterns must match hypotheses. But those hypotheses must be different.