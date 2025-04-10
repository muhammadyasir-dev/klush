# klush

!(logo)[/assets/klush.jpg]

klush is a dynmicaly typed object oriented programming language with garbage collector.
```
// Your first klush Program
print "not a fluff developer!";
```

**Head over to the [Documentation](/DOCUMENTATION.md)** to see code examples and other language features!


### installation 
```
## linux

export MY_PROGRAM_PATH="/downlaod/path/to/klush/"
```

```
source ~/.bashrc
```

## Windows

God knows how to set paths on trash windows.

## Under the hood

```
                   klush architecture
                
            ------------
           |  Compiler  |       <- Front End
            ------------
                  v
            ------------
           |  Bytecode  |       <- Representation
            ------------
                  v
          -----------------
         | Virtual Machine |    <- Execution
          -----------------
```

## The klush Language Spec

klush  grammar looks something like this, in order of associativity and precedence:

```
program        → statement* EOF ;

declaration    → classDecl
                 | funDecl
                 | varDecl
                 | statement ;

classDecl      → "class" IDENTIFIER ( "<" IDENTIFIER )?
                 "{" function* "}" ;             
                 
funDecl        → "fun" function ;

function       → IDENTIFIER "(" parameters? ")" block ;             

parameters     → IDENTIFIER ( "," IDENTIFIER )* ;
                 
varDecl        → "var" IDENTIFIER ( "=" expression )? ";" ;

statement      → exprStmt
                 | forStmt
                 | ifStmt
                 | printStmt
                 | returnStmt
                 | whileStmt
                 | block ;

returnStmt     → "return" expression? ";" ;

forStmt        → "for" "(" ( varDecl | exprStmt | ";" )
                 expression? ";"
                 expression? ")" statement ;

whileStmt      → "while" "(" expression ")" statement ;

ifStmt         → "if" "(" expression ")" statement
                 ( "else" statement )? ;

block          → "{" declaration* "}" ;

exprStmt       → expression ";" ;

printStmt      → "print" expression ";" ;

expression     → assignment ;

assignment     → ( call "." )? IDENTIFIER "=" assignment
                 | logic_or ;
               
logic_or       → logic_and ( "or" logic_and )* ;

logic_and      → equality ( "and" equality )* ;

equality       → comparison ( ( "!=" | "==" ) comparison )* ;

comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;

term           → factor ( ( "-" | "+" ) factor )* ;

factor         → unary ( ( "/" | "*" ) unary )* ;

unary          → ( "!" | "-" ) unary | call ;

call           → primary ( "(" arguments? ")" | "." IDENTIFIER )* ;

arguments      → expression ( "," expression )* ;

primary        → "true" | "false" | "nil" | "this"
               | NUMBER | STRING | IDENTIFIER | "(" expression ")"
               | "super" "." IDENTIFIER ;

```
