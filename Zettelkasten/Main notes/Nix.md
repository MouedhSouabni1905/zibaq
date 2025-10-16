## Nix Flakes 

**General structure of a `flake.nix` file :**
- It is an attribute set.
- Contains attributes: inputs, outputs (required), potentially description and nixConfig for advanced configuration options.
- The inputs defines the "sources" (urls to tarballs, github directories, filepaths, etc) from which packages will be fetched.
- Outputs is a function that takes as arguments a set of attributes (usually *self* and *nixpkgs*) and returns a set of attributes.
- This function defines multiple attributes, eg. `devShells` which is an attribute set where you can **use** the `mkShell` function, and when you run `nix develop` in the directory containing that flake, it will open nix shell like the one you defined in the `mkShell` function.
**Details :**
- You can think of nix flakes like the entry point of a repository, it declares the dependencies of a set of packages, and defines what is produced.
- Inputs specify the other flakes your flake depends on, it is an attribute set defining a few URLs or repos.
- Meaning if the source has a flake.nix (or default.nix) file in the root of the repository for example, it will automatically execute what is described in that file to build the package.
- The `self` is a special input that references the source tree of the current flake, allowing the output function to access other top-level attributes, like the inputs for example.
- Outputs define what your flake makes available.
- Think of the `flake.nix` file as just a **description** of the flake. The *flake* itself isn't the file, but what the file describes, ie. a set of nix derivations (eg. packages, devShells, ...).
- The definition of a derivation, in the nix reference manual: a specification for running an executable on precisely defined input files to repeatably produce output files at uniquely determined file system paths. It takes as input an attribute set, the attributes of which specify the inputs to the process. It outputs an attribute set, and produces a store derivation as a side effect of evaluation.
- [Other nix jargon definitions](https://nix.dev/manual/nix/2.22/glossary#glossary)

## Nix language

The basic building block of the nix language are nix expressions. A nix expression is *something that returns a result.* Basically, there can only be one nix expression in a single file. In the nix language, things that return results are values and functions. Values can be of any type possible, and can be referenced as the constants they are, or by their variable name. Variables can't be simply declared, they have to be defined, and variables can only be defined **inside** a nix expression using a let binding, otherwise the variable definition itself is the nix expression. This is crucial to understanding how the nix language works. You can nest expressions, but you can't make multiple different expressions in one file, **unless** they are part of an attribute set. You cannot assign to a variable the result of an invalid expression. An attribute set **needs** to have variables, so a set of constants is invalid, since it is like an associative (key => value) array. A normal array (list) is considered a value, like constants, anonymous functions and mathematical or string operations, as in they can't be passed as the argument to a function, or used as the return value of a function. A function will always return a **named and defined** object, and doesn't return the result of expressions. In the nix repl, you might be able to type constants, expression,. A function that is defined to wait for an attribute set needs an object defined as an attribute set, not an attribute set of already defined variables. When you assign a value, you cannot change its type later on.


```nix
mul = s@{ a, b, ... }: a _ b _ s.c; # 's' now refers to the entire input set
# '@' is used to bind an input attribute set to a name so that it can be used inside the function
outputs = { pkgs, ... } @ inputs: { ... }; # same concept
# variable = attrSet@attrSet : { function body }
```
By finding a parallel, we can understand what's going on:
We bind the pkgs variable from the first attribute set to the pkgs  in the inputs variable, and the `...` next to pkgs aids the destructuring by allowing to ignore the other attributes of the inputs set, and we bind the entire attribute set on the left to the attribute set on the right, all using this `@` operator. This input is then used inside the function and an attribute set is returned into the outputs variable.
Other example of the same concept:
```nix
nix-repl> f = {a,...}@b: a*a

nix-repl> f b
4
```
Having previously defined `a = 2` and `b = { a = a; }`.