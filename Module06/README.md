# Exploring For Loops, Lists, Tuples, Sets

For loops in python go hand in hand with data structures such as lists, and tuples. In this activity, we will explore both the for loop, and dive deeper into sequential data structures. 

### ⭐ Working in Teams ⭐
When working in teams, remember do not let one person do all the work. Make sure to work together, and ask questions. It is also better if different people program, and you all take turns programming for various team assignments.

### Learning Objectives

* Add `set` to the collection of structures that hold sequential data
* Be able to describe the difference between immutable (tuple) and mutable (lists)
* Be able to describe some of the memory concerns when working with lists and tuples
* Use a for loop to access sequential items
* Adding the `range` function to help with for loops and numeric access


### Adding Set

> [!TIP]
> A set in python is meant to mimic a mathematical set you are learning in CS 5002. It doesn't have
> any special notation, but used to keep a list of unique elements. The main difference is the
> use of curly brackets. 

As a quick reference, a set is a list (mutable) that can't have duplicates.

```python
good_guys = {"Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max"}
good_guys.add("Westley") # this will not add a duplicate
print(good_guys)
```




> [!WARNING]
> You cannot create an empty set using `val = {}` that actually creates something called a 
> dictionary which you will explore in the future. Instead, if you want the empty set,
> you would use  `val = set()`.

## Practice With the For (each/in) Loop

The for loop in python, is often called a for/in or for/each loop in other languages. The idea is:

```text
for (each) item in sequence
```

For this activity, you should work through the examples using your python interactive window. You will also want to have [python tutor] see how the memory is working. 

> [!WARNING]
> For loops in many languages are for number iteration. Python uses what is more commonly
> known as a 'for each' loop while calling it a for. Don't let it confuse you
> in the future when you see for loops vs. for each loops.

### For value in a list of values

Assume the following list:

```python
good_guys = ["Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max"]
```

for loops, allow you iterate over the list

```python
for character in good_guys:
    print(character)
```

This is the equivalent to saying

```python
counter = 0
while counter < len(good_guys)
    character = good_guys[counter]
    print(character)
    counter += 1
```

Run both in [python tutor] to see the difference in execution, even though they are equivalent in results. 

### :memo: Discussion
* What are some cases to use a for loop?
* What are some cases were a while loop is better (hint: when you don't have a sequence, but there may be other cases that come to mind)?

### Adding Range

Because it is common to run from $0..N$ python has a built in function called `range` that builds a tuple of numbers.

```python
for i in range(0,10):
    print(i)
```

Run the above code, see what happens. Is it inclusive / exclusive of values? You can also run the following to get an idea of what `range` is actually returning

```python
print(range(0,10))
```

> [!TIP]
> You can also add `step=n` where $n$ is a number, to skip numbers, you should feel free to explore.

Because range exists, we can start blurring the line between while and for loops. Simple counter increments are often best with a for loop. However, there are still cases where `while` shines. Think about the `run()` function in homework 05.
Your code may be different, this is just one way to write the run() function. 

## List, Tuple, Set, String
For loops work best on `sequential data` which is what we current know as 
* string 
* list
* tuple
* set


### Discussion:
* As a group talk about the differences between the four sequential data types. 
* Out of the four listed, which two are **immutable** and which two are **mutable**?

### Sequential Data and Mutability

Why does this term mutability matter for programming? Wouldn't it make sense to just use lists all the time? Often, many programs do just that, and by default many python functions return a list. 

However, when thinking about a **list** a computer not only has to keep memory for the values in the list, it also has to keep extra memory incase that list is expanded. While it depends on the language, it is often double that of what is in the list in worst case!

We can measure that in python by trying the following

```python
from sys import getsizeof
good_guys = ["Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max"]
size_of = getsizeof(good_guys)
print(size_of)
```

While it may vary a bit depending on the system and python version, when running this, the size was 104.

However, happens if we change it to a tuple?

```python
from sys import getsizeof
good_tuple = ("Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max")
size_of = getsizeof(good_tuple)
print(size_of)
```
The memory size dropped to 80. 

Why, because python knows the memory is fixed, so it doesn't have to keep additional information to allow values to be added or removed. Additionally, because the memory is fixed, it can also share memory between objects.

Try the following inside of a file, and then load the file.
```python
good_guys = ["Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max"]
good_guys_copy = ["Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max"]
id(good_guys)
id(good_guys_copy)
```

The `id` function tells you where the object is located in memory. 

while it will change between runs, the output when writing this up was
```
1882969788672
1882965039744
```
two different memory locations. Which makes sense, as they are two different lists that can be modified independently.

Now try the following by putting it into a python file and running it.
```python
good_tuple = ("Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max")
good_tuple_copy = ("Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max")
id(good_tuple)
id(good_tuple_copy)
```

The output when we ran it was
```
2869804528672
2869804528672
```
Yours will vary, and it may even be different depending on how you run the code. However, when you run it as an independent program, python is able to detect that these two variables are pointing to **immutable** items, and thus will just set the variables to the same memory location! This saves overall memory consumption. 

For reference, the memory could be diagramed as the following.

![Memory Model]

However, since strings are immutable, a more detailed representation would be.

![Memory Model Two]


However, that is a bit complicated, so strings just tend to be written as literals.

:memo: Discuss the above concepts. Why would it be beneficial to do all this?

## Let's dive deeper

Take the following program:

```python
from random import randint

names = ("Westley", "Buttercup", "Inigo Montoya", "Fezzik", "Miracle Max")

def get_name():
    return names[randint(0, len(names)-1)]


def build_copies(n:int ):
    lst = []
    for val in range(0, n):   
        if (val % 2) == 0:
            lst.append(get_name())
        else:
            lst.append(get_name()+"2")
    return lst


def get_mixed():
    return (["Vizzini", "Rugen", "Humperdinck"], names)
    

def build_complex_structure():
    lst = build_copies(3)
    mixed = get_mixed()
    lst.append(mixed)
    del mixed[0][0] # del removes an item from a list
    print(lst) 


if __name__ == "__main__":
    build_complex_structure()
```

:fire: Task: Draw the memory structure of what is going on. For tuples, place them together, and if you have more than one variable pointing towards the tuple, draw those areas to it.   You are free to use [python tutor], but for simplicity it will usually show strings as standard variables not values sitting on the 'heap'. There is a dropdown that will say 'store all objects on the heap', but it can be a bit overwhelming. 

> [!NOTE]
> We will explore the term heap and stack in CS 5008. It is memory specific to where the computer stores the information. For now, don't worry other than knowing immutable objects are often just references to the same item. 

### :memo: Discussion

* How many values are being duplicated as compared to using the same location in memory?

* How did the list inside of the tuple get modified? 
  * Hint: it is because it isn't copying, but storing a memory reference to the list. This is a great discussion topic to explore!
  * This is a common error, assuming things are copied all the time. 


## Why does this matter?

For now, the most important part is understanding the vocabulary. However, as you dive deeper into languages, you will find it matters. If things are immutable, it is often easier to work with them in cases of parallel processing and memory management, but they can be expensive if you have to modify them. This is a constant discussion in computers, speed vs. amount of memory to use. Computers can be infinitely fast, if memory was infinite but neither are true.


## Last Task: Work on Coding-Practice
Make sure to work on the [Coding Practice Problems](https://github.com/CS5001-khoury/Resources/blob/main/PracticeProblems.md). Have each member of your group pick a different problem, and you will all work on your problems. Make sure to discuss your solution with the team, and paste your code to your *teams* meeting channel / upload the python .py file! 

At the end of every Team Activity, you will be encouraged to work on coding practice problems as a team. It is important you take this time to talk about solutions, approaches, and make suggestions to each other! You are building a skill needed for technical interviews, and like all new skills it is important to practice.  Some times do the practice problems after the meeting, but then use the chat to comment. Either is fine, but it is important to get feedback and ask questions. 


## Submission
There is no "submission" for the Team Activity. Make sure you have your notes for the meeting (can be a doc in the files section) in your team's meeting channel. The TAs will check the attendance logs and award points based on attendance and completed notes. 



[python tutor]: https://pythontutor.com/python-debugger.html
[Memory Model]: memory_one.png
[Memory Model Two]: memory_two.png