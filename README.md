scheme-parser
=============

A parser in Scheme that will return the number of statements and maximum depth level of a given program.

The parser will report the number of statements and maximum depth level of a valid program defined as:

```
G = ( S, N, P, Σ) where
S = ( Program )
N = ( statement_list, statement, expr, symbol, op )
Σ = ( if, bool, then, while, id, const, =, +, -, *, / )
P = ( Program         -> statement_list
      statement_list  -> statement statement_list
                      -> statement
      statement       -> if bool then statement_list
                      -> while bool statement_list
                      -> id = expr
      expr            -> symbol op symbol
      symbol          -> id
                      -> const
      op              -> + | - | * | /
```


The program will be provided as an s-expression, so the following program:

```C
if bool then
  while bool
    id = id + const
    if bool then
      id = const / const
id = const * id
```

should be passed in as:

```C
((if bool then
  (while bool
    (id = id + const)
    (if bool then
      (id = const / const)
    )
  )
)
(id = const * id)
)
```

The invocation of the above program will be:
    
    (parser '((if bool then (while bool (id = id + const)(if bool then (id = const / const))))(id = const * id)))

###To run:
    $ mzscheme < parser.scm