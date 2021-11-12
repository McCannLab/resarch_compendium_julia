# Research compendium including code written in Julia
![Reproduce the analysis](https://github.com/McCannLab/resarch_compendium_julia/workflows/Reproduce%20the%20analysis/badge.svg)

This is a [template repository](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-template-repository), i.e. a repository that can be used to populate a repository when starting a new project from scratch. 

This repository includes: 
  1. a minimal example in `script.jl`
  2. A working workflow to test the code on [GitHub actions](https://github.com/features/actions).


:warning: Please, avoid long run when your project is private as we have a limited number of seconds per month for private repository.





## Style guide

This section describes the coding style rules preferred in the lab (NB this was started by @gabrielgellner). They are heavily based on the `JuMP` style guides, though there are exceptions.

### Formatting

Julia unfortunately does not have an autoformatting tool like
[gofmt](https://blog.golang.org/go-fmt-your-code). Until a reliable
autoformatting tool is available, we adopt the following conventions.

#### Whitespace

For conciseness, never use more than one blank line within a function, and never
begin a function with a blank line.

Bad:
```julia
function foo(x)
    y = 2 * x


    return y
end

function foo(x)

    y = 2 * x
    return y
end
```

Julia is mostly insensitive to whitespace characters within lines.
For consistency:

- Use spaces between binary operators (with some exceptions, see below)
- Use a single space after commas and semicolons
- Do not use extra spaces for unary operators, parentheses, or braces
- Indent within new blocks (except `module`) using 4 spaces

Good:
```julia
f(x, y) = [3 * dot(x, y); x']
```

Bad:
```julia
f(x,y) = [ 3*dot(x,y) ; x' ]
```

Good:
```julia
module Foo

function f(x)
    return x + 1
end

end # module Foo
```

##### Exceptions

We make an exception for the `:` operator when it is used to form a range.

Good:
```julia
x = 1:5
```

Bad:
```julia
x = 1 : 5
```

One reason is that it can be confused with Julia's conditional statement:
`cond ? x : y` which requires whitespace around the `:`.

Good:
```julia
2 * x  # This is preferred if space is not an issue.
2 * (x + 1)
```

Bad:
```julia
2(x + 1)
```

#### Return statements

To avoid situations in which it is unclear whether the author intended to return
a certain value or not, always use an explicit `return` statement to exit from a
function. If the return from a function is `nothing`, use `return` instead of
`return nothing`.

We make an exception for assignment-form one-line functions (`f(x) = 2 * x`).

Good:
```julia
foo(x) = 2 * x  # Acceptable if one line
function foo(x)
    return 2 * x
end
function foo!(x)
    x[1] += 1
    return
end
```

Bad:
```julia
function foo(x)
    2x
end
function foo!(x)
    x[1] += 1
    return nothing
end
```

#### Figure plotting

[PyPlot](https://github.com/JuliaPy/PyPlot.jl) is a nice option for plotting. Go [here](https://gist.github.com/gizmaa/7214002) for example coding with PyPlot.

To automatically open plots outside of Atom, disable the Plot Pane in the UI Options of the Juno Settings.

Whenever plotting a figure ensure that the code follows below:

```julia
    plot_name = figure()
    plot()
    plotoptions
    return plot_name
```

To ease figure creation, place plotting code in a let block.
 
