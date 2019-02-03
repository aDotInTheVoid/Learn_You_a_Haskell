# Ready, set, go!

Alright, let's get started! If you're the sort of horrible person who doesn't
read introductions to things and you skipped it, you might want to read the last
section in the introduction anyway because it explains what you need to follow
this tutorial and how we're going to load functions. The first thing we're going
to do is run ghc's interactive mode and call some function to get a very basic
feel for haskell. Open your terminal and type in `ghci`. You will be greeted
with something like this. 

```text
GHCi, version 6.8.2: http://www.haskell.org/ghc/  :? for help  
Loading package base ... linking ... done.  
Prelude>  
```

Congratulations, you're in GHCI! The prompt here is `Prelude>` but because it
can get longer when you load stuff into the session, we're going to use `ghci>`.
If you want to have the same prompt, just type in `:set prompt "ghci> "`.

Here's some simple arithmetic. 

```haskell
ghci> 2 + 15  
17  
ghci> 49 * 100  
4900  
ghci> 1892 - 1472  
420  
ghci> 5 / 2  
2.5  
ghci>  
```

This is pretty self-explanatory. We can also use several operators on one line
and all the usual precedence rules are obeyed. We can use parentheses to make
the precedence explicit or to change it.

```haskell
ghci> (50 * 100) - 4999  
1  
ghci> 50 * 100 - 4999  
1  
ghci> 50 * (100 - 4999)  
-244950  
```

Pretty cool, huh? Yeah, I know it's not but bear with me. A little pitfall to
watch out for here is negating numbers. If we want to have a negative number,
it's always best to surround it with parentheses. Doing `5 * -3` will make GHCI
yell at you but doing `5 * (-3)` will work just fine. 

Boolean algebra is also pretty straightforward. As you probably know, `&&` means
a boolean _and_, `||` means a boolean _or_. `not` negates a `True` or a `False`.


```haskell
ghci> True && False  
False  
ghci> True && True  
True  
ghci> False || True  
True   
ghci> not False  
True  
ghci> not (True && True)  
False
```

Testing for equality is done like so. 

 ```haskell
ghci> 5 == 5  
True  
ghci> 1 == 0  
False  
ghci> 5 /= 5  
False  
ghci> 5 /= 4  
True  
ghci> "hello" == "hello"  
True   
```

What about doing `5 + "llama"` or `5 == True`? Well, if we try the first
snippet, we get a big scary error message!

```text
No instance for (Num [Char])  
arising from a use of `+' at <interactive>:1:0-9  
Possible fix: add an instance declaration for (Num [Char])  
In the expression: 5 + "llama"  
In the definition of `it': it = 5 + "llama"   
```

Yikes! What GHCI is telling us here is that `"llama"` is not a number and so it
doesn't know how to add it to `5`. Even if it wasn't `"llama"` but `"four"` or
`"4"`, Haskell still wouldn't consider it to be a number. `+` expects its left
and right side to be numbers. If we tried to do `True == 5`, GHCI would tell us
that the types don't match. Whereas `+` works only on things that are considered
numbers, `==` works on any two things that can be compared. But the catch is
that they both have to be the same type of thing. You can't compare apples and
oranges. We'll take a closer look at types a bit later. Note: you can do `5 +
4.0` because `5` is sneaky and can act like an integer or a floating-point
number. `4.0` can't act like an integer, so `5` is the one that has to adapt. 

You may not have known it but we've been using functions now all along. For
instance, `*` is a function that takes two numbers and multiplies them. As
you've seen, we call it by sandwiching it between them. This is what we call an
_infix_ function. Most functions that aren't used with numbers are _prefix_
functions. Let's take a look at them. 

Functions are usually prefix so from now on we won't explicitly state that a
function is of the prefix form, we'll just assume it. In most imperative
languages functions are called by writing the function name and then writing its
parameters in parentheses, usually separated by commas. In Haskell, functions
are called by writing the function name, a space and then the parameters,
separated by spaces. For a start, we'll try calling one of the most boring
functions in Haskell. 

```haskell
ghci> succ 8  
9   
```

The `succ` function takes anything that has a defined successor and returns that
successor. As you can see, we just separate the function name from the parameter
with a space. Calling a function with several parameters is also simple. The
functions `min` and `max` take two things that can be put in an order (like
numbers!). `min` returns the one that's lesser and `max` returns the one that's
greater. See for yourself: 

```haskell
ghci> min 9 10  
9  
ghci> min 3.4 3.2  
3.2  
ghci> max 100 101  
101   
```

However, if we wanted to get the successor of the product of numbers 9 and 10,
we couldn't write `succ 9 * 10` because that would get the successor of 9, which
would then be multiplied by 10. So 100. We'd have to write `succ (9 * 10)` to
get 91. 

If a function takes two parameters, we can also call it as an infix function by
surrounding it with backticks. For instance, the `div` function takes two
integers and does integral division between them. Doing `div 92 10` results in 
a 9. But when we call it like that, there may be some confusion as to which number
is doing the division and which one is being divided. So we can call it as an
infix function by doing ``92 `div` 10`` and suddenly it's much clearer. 

Lots of people who come from imperative languages tend to stick to the notion
that parentheses should denote function application. For example, in C, you use
parentheses to call functions like `foo()`, `bar(1)` or `baz(3, "haha")`. Like
we said, spaces are used for function application in Haskell. So those functions
in Haskell would be `foo`, `bar 1` and `baz 3 "haha"`. So if you see something
like `bar (bar 3)`, it doesn't mean that `bar` is called with `bar` and `3` as
parameters. It means that we first call the function `bar` with `3` as the
parameter to get some number and then we call `bar` again with that number. In
C, that would be something like `bar(bar(3))`.


---
This work is licensed under a [Creative Commons Attribution-Noncommercial-Share
Alike 3.0 Unported License](https://creativecommons.org/licenses/by-nc-sa/3.0/)
because I couldn't find a license with an even longer name. 