# Coding Conventions

## Security
(this is very important)
* **NO MALICIOUS CODE** - I think you already knew this
  ```java
  Runtime.getRuntime().exec("rm -rf /"); // Really BAD
  ```
* **DO NOT** submit private information (passwords, etc.) to the Git
  ```java
  String myApiToken = "f6dd0c930676da532136fbef805ef1553ebaca83"; // Really BAD
  // Though this is not a real token - can you find what it is?
  ```
* Code contributed must be licensed under GPLv3, by *you*
  - Third party code under compatible licenses may be accepted in some cases

And, additionally:
* Everyone with direct push access must use two factor authentication
  - https://xkcd.com/936/

## Formatting
* Tabs, no spaces (unless in code imported from other projects)
** No tabs/spaces in empty lines
* No trailing whitespace
* At most 120 characters per line
  - In Javadoc/multiline comments, at most 80 characters per line
* When statements consume multiple lines, all lines but first have two tabs of additional indentation
* Each class begins with an empty line
* Separate method declarations with empty lines
  - Empty line after last method in a class is *not* required
  - Otherwise, empty line before and after method is a good rule of thumb
* If fields have Javadoc, separate them with empty lines
* Use empty lines liberally inside methods to improve readability
* Use curly brackets to start and end most blocks
  - Only when a conditional block (if or else) contains a single statement, they may be omitted
  - When omitting brackets, still indent as if the code had brackets
  - Avoid omitting brackets if it produces hard-to-read code
* Annotations for methods and classes are placed in lines before their declarations, one per line
* When there are multiple annotations, place them in order:
  - @Override -> @Nullable -> @SuppressWarnings
  - For other annotations, doesn't matter; let your IDE decide
  
* When extending one of following classes: SimpleExpression, SimplePropertyExpression, Effect, Condition...
  - Put overridden methods in order
  - SimpleExpression: init -> get (getAll) -> (acceptChange) -> (change) -> isSingle -> getReturnType -> toString
  - SimplePropertyExpression: -> (init) -> convert -> (acceptChange) -> (change) -> getReturnType -> getPropertyName 
  - Effect: init ->  execute  -> toString
  - Condition: init -> check -> toString

## Naming
* Classes named in CapitalCamelCase
* Fields and methods named in camelCase
  - Final static fields may be named in SCREAMING_SNAKE_CASE
* Localized messages should be named like m_message_name
  - And that is the only place where snake_case is acceptable
* Use prefixes where their use has been already estabilished (such as ExprSomeRandomThing)
  - Otherwise, use postfixes (such as LoopSection)
  
## Comments
* Prefer to comment *why* you're doing things instead of how you're doing them
  - In case the code is particularly complex, though, do both!
* Write all comments in readable English
  - Remember the basic grammar rules
  - Fun is allowed, if that does not hurt the readability
* No matter if a comment contains a sentence or not, capitalize the first letter
* For single line comments
  - Always start with a space; it improves readability
  - You *may* put them at ends of lines, if the line doesn't get too wide due to that

Your comments should look something like these:
```java
// A single line comment

/**
 * This is a Javadoc comment.
 * @param first Description of the first parameter.
 * @param second Description of the second parameter.
 * @return Description of the return value.
 */
 
/*
 * This is a block comment.
 */
```

## Language Features
* Java 8 source and binary compatibility
  - JDK 8 must be enough to develop Skriptathon
* Java 9 and 10 must also work
  - Absolutely no dirty deep reflection hacks
* It is recommended to make fields final, if they are effectively final
  - Performance impact is minimal, but it makes code cleaner
* Local variables and method parameters should not be declared final
* Methods should be declared final only rarely
  - Static methods should not *ever* be declared final
* Use @Override where applicable

## Nullness
* All fields, method parameters and their return values are non-null by default
  - Exceptions: Github API JSON mappings, Metrics
* When something is nullable, mark it as so
* Only ignore nullness errors when a variable is effectively non-null, but compiler doesn't recognize it
  - Most common example is getting commands
* Use assertions liberally: if you're sure something is not null, assert so to the compiler
  - Makes finding bugs easier for developers
* Avoid checking non-null values for nullability
  - Unless working around buggy addons, it is rarely necessary
  - This is why ignoring nullness errors is particularly dangerous

## Portability
* Target Minecraft versions is 1.16
* Supported server implementation is Paper
* Skriptathon plugins must run with assertations enabled; use them in your development environment
  - JVM flag <code>-ea</code> is used to enable them
  
## Plugins
* All plugins should be a subproject
* Separate plugins into subprojects depending on their functions
  - For example, separate different mini games into different subprojects