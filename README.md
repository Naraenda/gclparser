# GCL Parser

A simple parser for the GCL language used in the course _Program Verification_. The parser is written using Happy and Haskell. A Cabal build file is included to build the library.

This parser admits a richer language than the base GCL to also accommodate optional assignments. You can ignore the parts of the parser/syntax that you don't need in your parts of assignments.

#### Prerequisites
To compile the tool, the following package are required:
* array
* containers
* optparse-applicative
* pretty.

#### Compilation
To compile the library, run the command `cabal build`.

#### Running/testing from interpreter

After building (see above), you can run ghci from ./src, passing the path to where
Cabal puts the generated files, and passing relevant language options:

```
ghci -i../dist/build -XNamedFieldPuns
```

From there you can load packages e.g. `:l GCLParser.Parser` and try out functions defined there in the interpreter.

#### Usage

The module `GCLParser.Parser` exports two functions:

```Haskell
parseGCLstring :: String -> ParseResult Program
parseGCLfile :: FilePath -> IO (ParseResult Program)
```
The first is to parse a GCL program from a string, and the second is to parse from a text file. The parser returns a value of type `ParseResult Program`, which is a synonym for `Either String Program`. Such value takes the form of either `Left e` where `e` is an error message if the parsing fails, or `Right p` if the parsing is successful. In the later case, `p` is a value of type `Program` which is a datatype used to structurally repfresent a GCL program. See the module `GCLParser.GCLDatatype` for its definition.

Note that the module `GCLParser.Parser` is generated by Happy. The source code is `src/GCLParser/Parser.y`, which is a Happy parser definition. So, if you need to change the parser, you should not edit `Parser.hs` manually, but instead edit `Parser.y`.

**Pretty printing.** The module `GCLParser.PrettyPrint` provides a function to pretty print a value of type `Program`:

```Haskell
ppProgram2String :: Program -> String
```

#### Supported GCL syntax

See in `/docs`.

#### Error message

Unfortunately almost none. But if some of you know how to make Happy produces a more friendly error message, do let me know.

#### GCL examples and verification benchmark

See in `/examples`

#### Credits

Many thanks to Stefan Koppier for providing the initial implementation of the parser.

**Contributors:** Stefan Koppier, Wishnu Prasetya
