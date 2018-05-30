---
layout: post
title: Lists II: Copying Lists
---

Hola, hope everyone had a good holiday weekend. Let's discuss how to copy lists.

Copying lists comes up fairly frequently. The most inuitive way to copy a list is simply to assign (=) an existing list to our new list:

```python

ToDo_Monday = ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Tuesday = ToDo_Monday

print('ToDo_Monday: ',ToDo_Monday)
print('ToDo_Tuesday: ',ToDo_Tuesday) 

```

We've all had those days. This does what we might expect; both lists are the same:

```python
ToDo_Monday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Tuesday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry']
```

But here's the wrinkle - we've only pointed "ToDo_Tuesday" to the list "ToDo_Monday." I'll prove it to you. If I modify ToDo_Tuesday after the assignment, then print both lists:

```python
ToDo_Monday = ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Tuesday = ToDo_Monday

print('ToDo_Monday: ',ToDo_Monday)
print('ToDo_Tuesday: ',ToDo_Tuesday)

ToDo_Monday.append('Eat noodles')
print('ToDo_Tuesday: ',ToDo_Tuesday)
```

We get:

```python
ToDo_Monday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Tuesday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Tuesday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry', 'Eat noodles']
```

Sadness. So, all we've done is point ToDo_Tuesday to reference the same data as ToDo_Monday. We can't modify them independently. How else might we copy our lists? 

## By Slicing

The first method we'll use is by **Slicing**. Remember the **:** operator? It allows us to pull only some part of a given list, or **slice**. 

``` print(ToDo_Monday[1:3])```

Gives us elements indexed 1 and 2 (the 3 is not inclusive):

```['Buy Gas', 'Pick up laundry']```

Another use (conveniently) for slicing is to create a copy. If we don't enter indicies, we get a copy of the entire original list:

```python:
ToDo_Monday = ['Grocery Store', 'Buy Gas', 'Pick up laundry']
ToDo_Wednesday = ToDo_Monday[:]

ToDo_Monday.append('Eat noodles')

print("ToDo_Monday: ", ToDo_Monday)
print("ToDo_Wednesday: ", ToDo_Wednesday)
```
```python
ToDo_Monday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry', 'Eat noodles']
ToDo_Wednesday:  ['Grocery Store', 'Buy Gas', 'Pick up laundry']
```

So now, we've got an actual copy - the append operation to ToDo_Monday **does not** affect ToDo_Wednesday, so they're not referencing the same list. However, there's a wrinkle here too. Any lists *inside* our copied list are only referenced, so they suffer the same issue as before:

```python:
ToDo_Monday = ['Grocery Store', 'Buy Gas', ['Call Jim']]
ToDo_Thursday = ToDo_Monday[:]

ToDo_Monday[2].append('Call Doc')

print("ToDo_Monday: ", ToDo_Monday)
print("ToDo_Thursday: ", ToDo_Thursday)
```
```python:
ToDo_Monday:  ['Grocery Store', 'Buy Gas', ['Call Jim', 'Call Doc']]
ToDo_Thursday:  ['Grocery Store', 'Buy Gas', ['Call Jim', 'Call Doc']]
```

This is referred to as a **Shallow Copy**, as nested data structures are only referenced. 

## DeepCopy

What we need is a **Deep Copy**. No references, no nada - give me a fully functional copy of my original list:

```python
import copy

ToDo_Monday = ['Grocery Store', 'Buy Gas', ['Call Jim']]
ToDo_Friday = copy.deepcopy(ToDo_Monday)

ToDo_Monday[2].append('Call Doc')

print("ToDo_Monday: ", ToDo_Monday)
print("ToDo_Friday: ", ToDo_Friday)



```
And finally, voila, our fully seperate copy,
```
ToDo_Monday:  ['Grocery Store', 'Buy Gas', ['Call Jim', 'Call Doc']]
ToDo_Friday:  ['Grocery Store', 'Buy Gas', ['Call Jim']]
```
