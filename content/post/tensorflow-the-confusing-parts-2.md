+++
title = "Tensorflow: The Confusing Parts (2)"
date = 2018-08-06T00:47:19-04:00
draft = true

authors = ["Jacob Buckman"]
tags = ["Tensorflow"]
categories = ["Tutorial", "TFTCP"]

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true
summary = "Tutorial on variable scoping, saving, and loading in Tensorflow."

+++


*This post is the second of a series; click [here](https://jacobbuckman.com/post/tensorflow-the-confusing-parts-1/) for the previous post, or [here](https://jacobbuckman.com/categories/tftcp/) for a list of all posts in this series.*

## Naming and Scoping

### Naming Variables and Tensors

As we discussed in Part 1, every time you call `tf.get_variable()`, you need to assign the variable a new, unique name. Actually, it goes deeper than that: every tensor in the graph gets a unique name too. The name can be accessed explicitly with the `.name` property of tensors, operations, and variables. For the vast majority of cases, the name will be created automatically for you; for example, a constant node will have the name `Const`, and as you create more of them, they will become `Const_1`, `Const_2`, etc.[^0] You can also explicitly set the name of a node via the `name=` property, and the enumerative suffix will still be added automatically:

###### Code:
```python
import tensorflow as tf
a = tf.constant(0.)
b = tf.constant(1.)
c = tf.constant(2., name="cool_const")
d = tf.constant(3., name="cool_const")
print a.name, b.name, c.name, d.name
```
###### Output
```python
Const:0 Const_1:0 cool_const:0 cool_const_1:0
```

Explicitly naming nodes is nonessential, but can be very useful when debugging. Oftentimes, when your Tensorflow code crashes, the error trace will refer to a specific operation. If you have many operations of the same type, it can be tough to figure out which one is problematic. By explicitly naming each of your nodes, you can get much more informative error traces, and identify the issue more quickly.

### Using Scopes

As your graph gets more complex, it becomes difficult to name everything by hand. Tensorflow provides the `tf.variable_scope` object, which makes it easier to organize your graphs by subdividing them into smaller chunks. By simply wrapping a segment of your graph creation code in a `with tf.variable_scope(scope_name):` statement, all nodes created will have their names automatically prefixed with the `scope_name` string. Additionally, these scopes stack; creating a scope within another will simply chain the prefixes together, delimited by a forward-slash.

###### Code:
```python
import tensorflow as tf
a = tf.constant(0.)
b = tf.constant(1.)
with tf.variable_scope("first_scope"):
  c = a + b
  d = tf.constant(2., name="cool_const")
  coef1 = tf.get_variable("coef", [], initializer=tf.constant_initializer(2.))
  with tf.variable_scope("second_scope"):
    e = coef1 * d
    coef2 = tf.get_variable("coef", [], initializer=tf.constant_initializer(3.))
    f = tf.constant(1.)
    g = coef2 * f
    
print a.name, b.name
print c.name, d.name
print e.name, f.name, g.name
print coef1.name
print coef2.name

```
###### Output
```python
Const:0 Const_1:0
first_scope/add:0 first_scope/cool_const:0
first_scope/second_scope/mul:0 first_scope/second_scope/Const:0 first_scope/second_scope/mul_1:0
first_scope/coef:0
first_scope/second_scope/coef:0
```

Notice that we were able to create two variables with the same name - `coef` - without any issues! This is because the scoping transformed the names into `first_scope/coef:0` and `first_scope/second_scope/coef:0`, which are distinct.



[^0]: There will also be a suffix `:device_num` added to the tensor names. For now, that's always `:0`, meaning the tensor is stored on device 0; using multiple devices will be covered in a future post.
