# MetaModelica.jl

This package replicates the runtime of the programming language MetaModelica. It also exposes
other packages that are a part of this runtime such as ImmutableList.jl

MetaModelica supports a powerfull but expensive mechanism for pattern matching called matchcontinue
This is provided by an extension of Rematch.jl

# Patterns:

    * `_` matches anything
    * `foo` matches anything, binds value to `foo`
    * `foo(__)` wildcard match on all subfields of foo, binds value to `foo`
    * `Foo(x,y,z)` matches structs of type `Foo` with fields matching `x,y,z`
    * `Foo(x=y)` matches structs of type `Foo` with a field named `x` matching `y`
    * `[x,y,z]` matches `AbstractArray`s with 3 entries matching `x,y,z`
    * `(x,y,z)` matches `Tuple`s with 3 entries matching `x,y,z`
    * `[x,y...,z]` matches `AbstractArray`s with at least 2 entries, where `x` matches the first entry, `z` matches the last entry and `y` matches the remaining entries.
    * `(x,y...,z)` matches `Tuple`s with at least 2 entries, where `x` matches the first entry, `z` matches the last entry and `y` matches the remaining entries.
    * `_::T` matches any subtype (`isa`) of T
    * `x || y` matches values which match either `x` or `y` (only variables which exist in both branches will be bound)
    * `x && y` matches values which match both `x` and `y`
    * `x where condition` matches only if `condition` is true (`condition` may use any variables that occur earlier in the pattern eg `(x, y, z where x + y > z)`)
    * `x => y` is syntactic sugar for `cons(x,y)` [Preliminary]
    * Anything else is treated as a constant and tested for equality

 * Patterns can be nested arbitrarily.

 * Repeated variables only match if they are `==` eg `(x,x)` matches `(1,1)` but not `(1,2)`.
 
 # Optional types:
 This package also support optionals (`Optional{T}`) in the same way as MetaModelica and can be used with `@match` and `@matchcontinue` above. The two available operations are `NONE` and `SOME(X)` where X is some datatype
 
 And much much more...
