# Learn You a Haskell for Great Good! 

## Chapter 1
* In purely functional programming you don’t tell the computer what to do as such but rather you tell it what stuff is. 
* So in purely functional languages, a function has no side-effects. The only thing a function can do is calculate something and return it as a result. That’s called referential transparency 
* Haskell is lazy. That means that unless specifically told otherwise, Haskell won’t execute functions and calculate things until it’s really forced to show you a result. That goes well with referential transparency and it allows you to think of programs as a series of transformations on data. It allows cool things such as infinite data structures.
* Haskell is statically typed. 
* Haskell uses a very good type system that has type inference. That means that you don’t have to explicitly label every piece of code with a type because the type system can intelligently figure out a lot about it. 
* GHC and Hugs are Haskell compilers. GHCi : ``docker run -it --rm -v $PWD:/src  haskell:8``
## Chapter 2
* GHCi can perform math operations (``+-*/``) but beware negative numbers must be wrapped in parenthesis.
* GHCi supports boolean algebra
* the ``==`` operation can be applied to everything that has the same type 
* the ``+-*/`` operations apply only to numbers
### Functions
* functions can be 
    * infix: ex 1 + 2. The function name is specified in the middle of the parameters
    * prefix: ex foo 1 2. The function name is prefixed before the paramenters
* Function application (prefix functions with the parameters) has the highest precedence of operations (infix functions)  
* If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks. 
    * ``8 `div` 3``
* if statement it is an expression that is defined as a piece of code that returns a value. 
* since it is an expression if statement must always have a then and an else. 
* functions can’t begin with a capitalised letter. 
* when a function doesn’t take any parameter it is called definition or name.
### Lists
* In Haskell lists are homogeneous data structure, they store elements of the same type.
* let lostNumbers = [4 ,8 ,15 ,16 ,23 ,48] (in GHCi let assign a name to a value) creates a list 
* ``++`` operator concatenate 2 lists and it walks through the list to concatenate with the second list (O(N)) 
    * ``[1,2] ++ [9,10] == [1,2,9,10]``
* ``:`` operator named cons prefix an element to the list and it is immediate (O(1)) 
    * ``5:[1 ,2 ,3 ,4 ,5] == [5,1,2,3,4,5]``
* ``[1,2,3]`` is actually just syntactic sugar for ``1:2:3:[]``
* If you want to get an element out of a list by index, use ``!!``. The indices start at 0. 
    * ``"Steve Buscemi" !! 6 — ‘B’``
* list of list must contain the same types
* Lists can be compared if the stuff they contain can be compared. 
    * ``[3,2,1] > [2,1,0] == True``
* function operating on the list
    * __head__ _list_ - returns the first element of a list
    * __tail__ _list_ -  returns the list without the first element 
    * __last__ _list_ -  returns the last element 
    * __init__ _list_ -  returns a list without the last element
    * __length__ _list_ -  returns the length of a list 
    * __null__ _list_ -  checks if a list is empty
    * __reverse__ _list_ -  returns a reversed list
    * __take__ _num list_ - returns a list with the first num element of the original list.
    * __drop__ _num list_ - returns a list without the first num element of the original list.
    * __maximum__ _list_ - return the maximum element of the list (only for comparable types)
    * __minimum__  _list_ - return the minimum element of the list (only for comparable types)
    * __sum__ _list_ - return the sum of a list of numbers
    * __product__ _list_ - return the product of a list of numbers
    * __elem__ _thing list_ - returns True if thing is an element contained in the list.
### Texas ranges
 * Ranges are a way of making lists that are arithmetic sequences of elements that can be enumerated.
    * ``[1..20] == [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]``
    * ``[’a’..’z’] == "abcdefghijklmnopqrstuvwxyz"``
 * Ranges can specify steps separating the first two elements with a comma and then specifying what the upper limit is:
    * ``[2 ,4..20] == [2,4,6,8,10,12,14,16,18,20]``
    * ``[20,19..1] == [20,19,18,17,16,15,14,13,12,11,10,9,8,7,6,5,4,3,2,1]``
 * Watch out when using floating point numbers:
    * ``[0.1 , 0.3 .. 1] == [0.1 ,0.3 ,0.5 ,0.7 ,0.8999999999999999 ,1.0999999999999999]``
 * Do not specify the upper limit for infinite lists
    * ``[13,26..]``
 * Functions that produce infinite lists:
    * __cycle__ _list_ - returns an infinite list cycling the list
       * ``take 10 (cycle [1,2,3]) == [1,2,3,1,2,3,1,2,3,1]``
    * __repeat__ _element_ - returns an infinit list of the same element
       * ``take 10 (repeat 5) == [5,5,5,5,5,5,5,5,5,5]``
### List comprehension
 * A list comprehension is composed by three parts: the output function, the input list and the predicate. The list comprehension is wrapped by squared brackets []
    * ``[x\*2 | x <- [1..10], x <= 12] == [2,4,6,8,10,12]``
    * ``length’ xs = sum [1 | _ <- xs]``
 * When a list comprehension has multiple predicates an element must satisfy all of them
    * ``[ x | x <- [10..20], x /= 13, x /= 15, x /= 19] == [10 ,11 ,12 ,14 ,16 ,17 ,18 ,20]``
 * When a list comprehension has several lists comprehensions produce all combinations of the given lists and then join them by the output function we supply.
    * ``[ x\*y | x <- [2,5,10], y <- [8,10,11]] == [16 ,20 ,22 ,40 ,50 ,55 ,80 ,100 ,110]``
    * ``[ x\*y | x <- [2,5,10], y <- [8,10,11], x\*y > 50] == [55 ,80 ,100 ,110]``
### Tuples
  * Tuples store a predefined number of values that may be not homogeneus on the type. Tuples can't contain an infinite number of items.
  * Tuples can contain lists
  * A tuple with two elements is called pair.
  * functions operating on tuples:
    * __fst__ _pair_ - returns the first component of a pair
      * ``fst (8 ,11) == 8``
    * __snd__ _pair_ - returns the second component of a pair
      * ``snd (8 ,11) == 11``
    * __zip__ _list list_ - It takes two lists and then zips them together into one list by joining the matching elements into pairs.
      * ``zip [1,2,3,4,5] [5,5,5,5,5] == [(1 ,5) ,(2 ,5) ,(3 ,5) ,(4 ,5) ,(5 ,5)]``
      * ``zip [5,3,2,6,2,7,2,5,4,6,6] ["im","a","turtle"] == [(5,"im"),(3,"a"),(2,"turtle")]``
## Chapter 3 - Type and Typeclasses
 * A type is a kind of label that every expression has.
 * Haskell has a static type system with type inference.
 * Explicit types starts with a letter in capital case.
 * ``::`` can be read as "has type off" and when using ``:t`` command in GHCi it separate the value from its type.
 * Square brackets denotes a list 
    * [Char] is of type *List of char* 
    * (True, ’a’) is of different type than (True, 2)
 * Functions also have types. When writing our own functions, we can choose to give them an explicit type declaration.
 * Common types in Haskell:
    * Int: bounded integer with a minumum and a maximum (for 32bits machines 2147483647 -2147483648).
    * Integer: unbounded integer for really big numbers but less efficient than Int.
    * Float: real floating point with single precision
    * Double: real floating point with double precision
    * Bool: boolean (True, False)
    * Char: represents a character. It’s denoted by single quotes. A list of characters is a String.
    * (): Empty tuple with a single value
### Type Variables
 * Type varaibles are variable that can be any possible type. They are similar to the generics concepts and allow to write generic functions that are not using any specific behabvior of the type.
 * Function that have type variabgles are called **polimorphic functions**.
### Typeclasses
 * A typeclass is similar to an interface that defines a behavior of a class. 
    * if a type is a part of a typeclass than it supports and implements the behavior that the typeclass describes
 * If a function is comprised only of special characters, it’s considered an infix function by default.
 * Everything before the => symbol is called a class constraint.
    * Example: equals function ```(==) :: (Eq a) => a -> a -> Bool``` that means: the equality function takes any two values that are of the same type and returns a Bool. The type of those two values must be a member of the Eq class (this was the class constraint).
 * Basic typeclasses:
    * ``Eq`` used for type supporting equality. It force to implement the functions ``==`` and ``/=``.
    * ``Ord`` is for types suppoprting ordering. ```(>) :: (Ord a) => a -> a -> Bool```.
      * Functions: ``>, <, >=`` and ``<=``. The ``compare`` function takes two ``Ord`` members and return an ``Ordering`` type that is represented by ``GT``, ``LT``, ``EQ``.\
      * To be member of ``Ord`` a type must be also member of ``Eq``.
  * ``Show`` used for types that can be represented as strings. The functions to be implemented is ``show`` that takes a generice type and returns a string.
  * ``Read`` used for types that can return a type from a ``String``. The function to be implemented is ``read``. ```read :: (Read a) => String -> a```
      * Example:  ```read "8.2" + 3.8``` returns ```12.0```.
  * ``Enum`` used for types sequentially ordered that can be enumerated. It can be used in list ranges in which are defined predecessor and successor with the ``pred`` and ``succ`` functions.
      * Types in this class: ``(), Bool, Char, Ordering, Int, Integer, Float and Double.
## Comments
 * The book avoid cautiously the word **object**. When it needs to describe the instance of a type, it uses **stuff**, **things**,etc. but never objects. It feels a bit weird to read at page 15: _"Lists can be compared if the stuff they contain can be compared."_ or at page 10: _"Whereas + works only on things that are considered numbers, == works on any two things that can be compared."_
## Errata Corrige
* page 15 (typo): hail instead of head
* page 25 (old info): Unlike Java or Pascal, Haskell has type inference.
