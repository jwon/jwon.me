---
title: "Python's Mutable Default Argument"
date: 2019-04-17 23:00:00 +0000
subtitle: "A quirk of Python you may have run into"
tags:
- Python
---
## Intro
If you've written a lot of Python code, you might have run into one of Python's quirks, the **Mutable Default Argument**. 

"What is that," you ask?

Take a look at this code:
```python3
def add_to_basket(item, basket=[]):
    basket.append(item)
    return basket
```
A reasonable implementation to add arbitrary items to a basket. It uses keyword arguments to provide a default value for `basket` if it is not passed in.
<!--more-->
However, you would quickly realize that this does not give you the intended effect:
```python3
>>> add_to_basket('banana')
['banana']
>>> add_to_basket('apple')
['banana', 'apple']
```
It should be creating a new basket every time since the `basket` keyword parameter is not passed in, but instead it seems like the default list paramter is only created once rather than on every invocation.

This is a "feature" of Python called Mutable Default Arguments.

There is a great thread on Stack Overflow that [discusses this][1] and the official Python documentation actually [covers this][2] as well:

(emphasis added)

> Default parameter values are evaluated from left to right when the function definition is executed. **This means that the expression is evaluated once, when the function is defined, and that the same “pre-computed” value is used for each call.** This is especially important to understand when a default parameter is a mutable object, such as a list or a dictionary: if the function modifies the object (e.g. by appending an item to a list), the default value is in effect modified. This is generally not what was intended. A way around this is to use None as the default, and explicitly test for it in the body of the function...

## So what can you do about this?

The easiest thing to do is to make the default parameter's value `None`. Like so:
```python3
def add_to_basket(item, basket=None):
    if basket is None:
        basket = []
    basket.append(item)
    return basket
```

I personally like a similar flavor to the above solution; something like:
```python3
def add_to_basket(item, basket=None):
    basket = basket or []
    basket.append(item)
    return basket
```
This works, but if something is passed into `basket` that has a `False`-y value (e.g. empty string (`''`) or empty dictionary (`{}`)), it will still return the default list value. I usually don't have to worry about this, so I like using the `or` notation.

## Conclusion
Hopefully this gives you a better idea of the gotcha in Python. It's one of those things where if you've never seen it before, could be very disorientating.

[1]: https://stackoverflow.com/q/1132941
[2]: https://docs.python.org/3/reference/compound_stmts.html#function-definitions
