strongly typed language developed by Microsoft.

# data types
## Value
- int
- float
- bool
- char
## Reference 
- string
- object
- dynamic
## namespaces
- system
- System.Collection.Generic

Something interesting, is that a `string` is a variable, meanwhile a `String` is a complex object that has multiple functions as iterating over it, lambda functions...


# Access modifiers
if no modifier is aplied, it will be private
## public
anyone on the solution can access it
## private
only the same class will access it
## protected
only from the same classes and derivates
## internal
withing the same assembler/ from the same DLL / from the same project

# events
any type of change. Delegates are the responses of events

# Modifiers
## static
they will always remain, never be garbage collected. Don't have to be instanced

## errors
`throw` vs `throw ex` will give you different outcomes, as throw will maintain the same stack trace meanwhile throw ex will create a new one 