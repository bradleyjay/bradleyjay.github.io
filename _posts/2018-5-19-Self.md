---
layout: post
title: Self - what is it, why do I care?
---

Happy Saturday! Let's talk about **self**. No, not me, *your* self - nevermind.

Why is the **self** argument required in a method, and what good does it do me? First, some context. My program has a menu class for users to make a selection:
  
  print("1) Thing 1" + "\n 2) Thing 2" + "\n 3) Thing 3")
  choice = input("Select one:")
  build(choice)

The user enters a number, and the module then calls this class' method **build()**. When build() is called, however, Python returns:

  build() takes 1 positional argument but 2 were given
  
What gives? We only included one argument.

Well, kind of. We included only one *explicit* argument. That's not all that's going on here. Methods by definition include an implicit *self* argument when called, in addition to what's explicitly passed. **build()** always passes the **self** argument at minimum. Behind the scenes, build(choice) really looks like (and remember, "object" is the instance of our class here)

Class.build(object, choice)

Two arguements! This "object" is usually refered to as self. So why do we care? This is great: **Self** represents a class instance from inside itself. That means we have convienent access to an instance's attributes and methods from inside the build() method. Anything my Object has as an attribute, build() can use with the syntax **self.attribute**, or methods with **self.method()**.



