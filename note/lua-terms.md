# Terms

## What is "chunk"?

> Each piece of code that Lua executes, such as a file or a single line in interactive mode, is a chunk. More specifically, a chunk is simply a sequence of statements.

## What is "closure"?

> While the registry implements global values, the upvalue mechanism implements an equivalent of C static variables, which are visible only inside a particular function. Every time you create a new C function in Lua, you can associate with it any number of upvalues; each upvalue can hold a single Lua value. Later, when the function is called, it has free access to any of its upvalues, using pseudo-indices.   
> We call this association of a C function with its upvalues a closure. Remember that, in Lua code, a closure is a function that uses local variables from an outer function. A C closure is a C approximation to a Lua closure. One interesting fact about closures is that you can create different closures using the same function code, but with different upvalues.
