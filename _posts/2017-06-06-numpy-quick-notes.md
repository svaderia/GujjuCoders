---
layout: post
title: Numpy Quick notes
author: sym
tags: [Python]
image: /assets/python.png
---

**Numpy** library provides you with an array data structure that holds some benefits over Python lists, 
such as: being more compact, faster access in reading and writing items, being more convenient and more efficient.
NumPy is a Python library that is the core library for scientific computing in Python. It contains a collection of 
tools and techniques that can be used to solve on a computer mathematical models of problems in Science and Engineering. 
One of these tools is a high-performance multidimensional array object that is a powerful data structure for 
efficient computation of arrays and matrices.


It's a pretty long guide, but covers almost everything you 
need to know, in the beginning, about Numpy. So be patient.
## Creating Arrays

```python
#creating arrays
>>> np.zeros(10, dtype='int')
array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])


#creating a 3 row x 5 column matrix
>>> np.ones((3,5), dtype=float)
array([[ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.]])


#creating a matrix with a predefined value
>>> np.full((3,5),1.23)
array([[ 1.23,  1.23,  1.23,  1.23,  1.23],
      [ 1.23,  1.23,  1.23,  1.23,  1.23],
      [ 1.23,  1.23,  1.23,  1.23,  1.23]])


#create an array with a set sequence
>>> np.arange(0, 20, 2)
array([0, 2, 4, 6, 8,10,12,14,16,18])


#create an array of even space between the given range of values
>>> np.linspace(0, 1, 5)
array([ 0., 0.25, 0.5 , 0.75, 1.])


#create a 3x3 array with mean 0 and standard deviation 1 in a given dimension
#Draw random samples from a normal (Gaussian) distribution.
>>> np.random.normal(0, 1, (3,3))
array([[ 0.72432142, -0.90024075,  0.27363808],
      [ 0.88426129,  1.45096856, -1.03547109],
      [-0.42930994, -1.02284441, -1.59753603]])

#create a 3x3 array with mean 0 and standard deviation 1 in a given dimension
#Draw random samples from a “standard normal” distribution.
>>> np.random.randn(2, 4)
array([[-4.49401501,  4.00950034, -1.81814867,  7.29718677], 
       [ 0.39924804,  4.68456316,  4.99394529,  4.84057254]]) 

#create an identity matrix
>>> np.eye(3)
array([[ 1.,  0.,  0.],
      [ 0.,  1.,  0.],
      [ 0.,  0.,  1.]])


#set a random seed
>>> np.random.seed(0)
>>> x1 = np.random.randint(10, size=6) #one dimension
>>> x2 = np.random.randint(10, size=(3,4)) #two dimension
>>> x3 = np.random.randint(10, size=(3,4,5)) #three dimension
>>> print("x3 ndim:", x3.ndim)
('x3 ndim:', 3)
>>> print("x3 shape:", x3.shape)
('x3 shape:', (3, 4, 5))
>>> print("x3 size: ", x3.size)
('x3 size: ', 60)
```

  
## Load Numpy arrays from text

```python
# This is your data in the text file
# Value1  Value2  Value3
# 0.2536  0.1008  0.3857
# 0.4839  0.4536  0.3561
# 0.1292  0.6875  0.5929
# 0.1781  0.3049  0.8928
# 0.6253  0.3486  0.8791

# Import your data
>>> x1, x2, x3 = np.loadtxt('data.txt',
                        skiprows=1,
                        unpack=True)
```
In the code above, you use `loadtxt()` to load the data in your environment. You see that the first argument 
that both functions take is the text file `data.txt`. Next, there are some specific arguments for each: in the first statement, 
you skip the first row and you return the columns as separate arrays with `unpack=TRUE`. 
This means that the values in column `Value1` will be put in `x1`, and so on.

Note that, in case you have `comma-delimited` data or if you want to specify the data type, 
there are also the arguments `delimiter` and `dtype` that you can add to the `loadtxt()` arguments.

Let’s take a look at your second file with data:
```python
# Your data in the text file
# Value1  Value2  Value3
# 0.4839  0.4536  0.3561
# 0.1292  0.6875  MISSING
# 0.1781  0.3049  0.8928
# MISSING 0.5801  0.2038
# 0.5993  0.4357  0.7410

>>> my_array2 = np.genfromtxt('data2.txt',
                         skip_header=1,
                         filling_values=-999)
```
You see that here, you resort to `genfromtxt()` to load the data. In this case, you have to handle some missing values 
that are indicated by the `MISSING` strings. Since the `genfromtxt()` function converts character strings in 
numeric columns to `nan`, you can convert these values to other ones by specifying the `filling_values` argument.
In this case, you choose to set the value of these missing values to `-999`.

If, by any chance, you have values that don’t get converted to `nan` by `genfromtxt()`, 
there’s always the `missing_values` argument that allows you to specify what the missing values of your data exactly are.

**Tip:** check out [this page](https://docs.scipy.org/doc/numpy/reference/generated/numpy.genfromtxt.html#numpy.genfromtxt) to 
see what other arugments you can add to import your data successfully.

The examples indicated this maybe implicitly, but, in general, `genfromtxt()` gives you a little bit more flexibility; 
It’s more robust than `loadtxt()`.

## Save Numpy arrays
Once you have done everything that you need to do with your arrays, you can also save them to a file. 
If you want to save the array to a text file, you can use the `savetxt()` function to do this:
```python
>>> import numpy as np
>>> x = np.arange(0.0,5.0,1.0)
>>> np.savetxt('test.out', x, delimiter=',')
```
Check out the functions in the table below if you want to get your data to binary files or archives:

|save()|	Save an array to a binary file in NumPy .npy format|
|savez()|	Save several arrays into an uncompressed .npz archive|
|savez_compressed()|	Save several arrays into a compressed .npz archive|

## Inspecting Numpy arrays
```python
# Print the number of `my_array`'s dimensions
>>> print(my_array.ndim)

# Print the number of `my_array`'s elements
>>> print(my_array.size)

# Print information about `my_array`'s memory layout
>>> print(my_array.flags)

# Print the length of one array element in bytes
>>> print(my_array.itemsize)

# Print the total consumed bytes by `my_array`'s elements
>>> print(my_array.nbytes)

# Print the length of `my_array`
>>> print(len(my_array))

# Change the data type of `my_array`
>>> my_array.astype(float)
```


## Array Indexing
The important thing to remember that indexing in python 
starts from zero.

```python
>>> x1 = np.array([4, 3, 4, 4, 8, 4])
>>> x1
array([4, 3, 4, 4, 8, 4])

#assess value to index zero
>>> x1[0]
4

#assess fifth value
>>> x1[4]
8

#get the last value
>>> x1[-1]
4

#get the second last value
>>> x1[-2]
8

#in a multidimensional array, we need to specify row and column index
>>> x2
array([[3, 7, 5, 5],
      [0, 1, 5, 9],
      [3, 0, 5, 0]])

#1st row and 2nd column value
>>> x2[2,3]
0

#3rd row and last value from the 3rd column
>>> x2[2,-1]
0


#replace value at 0,0 index
>>> x2[0,0] = 12
>>> x2
array([[12,  7,  5,  5],
      [ 0,  1,  5,  9],
      [ 3,  0,  5,  0]])
```


## Array Slicing
```
a[start:end] # items start through the end (but the end is not included!)
a[start:]    # items start through the rest of the array
a[:end]      # items from the beginning through the end (but the end is not included!)
```
```python
>>> x = np.arange(10)
>>> x
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])


#from start to 4th position
>>> x[:5]
array([0, 1, 2, 3, 4])


#from 4th position to end
>>> x[4:]
array([4, 5, 6, 7, 8, 9])


#from 4th to 6th position
>>> x[4:7]
array([4, 5, 6])


#return elements at even place
>>> x[ : : 2]
array([0, 2, 4, 6, 8])

#return elements from first position step by two
>>> x[1::2]
array([1, 3, 5, 7, 9])


#reverse the array
>>> x[::-1]
array([9, 8, 7, 6, 5, 4, 3, 2, 1, 0])
```

## Array Indexing
When it comes to NumPy, there are boolean indexing and advanced or “fancy” indexing.
First up is boolean indexing. Here, instead of selecting elements, rows or columns based on index number, you select those values from your array that fulfill a certain condition.

```python
# Try out a simple example
>>> print(my_array[my_array<2])

# Specify a condition
>>> bigger_than_3 = (my_3d_array >= 3)

# Use the condition to index our 3d array
>>> print(my_3d_array[bigger_than_3])
```
Note that, to specify a condition, you can also make use of the logical operators `|` (OR) and `&` (AND).

When it comes to fancy indexing, that what you basically do with it is the following: you pass a list or an array of integers to specify the order of the subset of rows you want to select out of the original array.
Does this sound a little bit abstract to you?
No worries, just try it out in the code chunk below:
```python
>>> print(my_2d_array) 
array([[1 2 3 4]
       [5 6 7 8]])
# Select elements at (1,0), (0,1), (1,2) and (0,0)
>>> print(my_2d_array[[1, 0, 1, 0],[0, 1, 2, 0]])
array([5 2 7 1])

# Select a subset of the rows and columns
>>> >>> print(my_2d_array[[1, 0, 1, 0]][:,[0,1,2,0]])
array([[5 6 7 5]
       [1 2 3 1]
       [5 6 7 5]
       [1 2 3 1]])
```
Now, the second statement might seem to make less sense to you at first sight. This is normal. It might make more sense if you break it down:
* If you just execute my_2d_array[[1,0,1,0]], the result is the following:
```python
array([[5, 6, 7, 8],
       [1, 2, 3, 4],
       [5, 6, 7, 8],
       [1, 2, 3, 4]])
```
* What the second part, namely, `[:,[0,1,2,0]]`, is tell you that you want to keep all the rows of this result, but that you want to change the order of the columns around a bit. You want to display the columns 0, 1, and 2 as they are right now, but you want to repeat column 0 as the last column instead of displaying column number 3. This will give you the following result:
```python
array([[5, 6, 7, 5],
       [1, 2, 3, 1],
       [5, 6, 7, 5],
       [1, 2, 3, 1]])
```

## Array Concatenation
```python
#You can concatenate two or more arrays at once.
>>> x = np.array([1, 2, 3])
>>> y = np.array([3, 2, 1])
>>> z = [21,21,21]
>>> np.concatenate([x, y,z])
array([ 1,  2,  3,  3,  2,  1, 21, 21, 21])


#You can also use this function to create 2-dimensional arrays.
>>> grid = np.array([[1,2,3],[4,5,6]])
>>> np.concatenate([grid,grid])
array([[1, 2, 3],
      [4, 5, 6],
      [1, 2, 3],
      [4, 5, 6]])


#Using its axis parameter, you can define row-wise or column-wise matrix
>>> np.concatenate([grid,grid],axis=1)
array([[1, 2, 3, 1, 2, 3],
      [4, 5, 6, 4, 5, 6]])
```
Until now, we used the concatenation function of arrays of equal dimension. But, what if you are required to combine a 2D array with 1D array? In such situations, `np.concatenate` might not be the best option to use. Instead, you can use `np.vstack` or `np.hstack` to do the task. Let's see how!
```python
>>> x = np.array([3,4,5])
>>> grid = np.array([[1,2,3],[17,18,19]])
>>> np.vstack([x,grid])
array([[ 3,  4,  5],
      [ 1,  2,  3],
      [17, 18, 19]])


#Similarly, you can add an array using np.hstack
>>> z = np.array([[9],[9]])
>>> np.hstack([grid,z])
array([[ 1,  2,  3,  9],
      [17, 18, 19,  9]])
```
Also, we can split the arrays based on pre-defined positions. Let's see how!
```python
>>> x = np.arange(10)
>>> x
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])


>>> x1,x2,x3 = np.split(x,[3,6])
>>> print x1,x2,x3
[0 1 2] [3 4 5] [6 7 8 9]

>>> grid = np.arange(16).reshape((4,4))
>>> grid
>>> upper,lower = np.vsplit(grid,[2])
>>> >>> print (upper, lower)
(array([[0, 1, 2, 3],
       [4, 5, 6, 7]]), 
 array([[ 8,  9, 10, 11],
       [12, 13, 14, 15]]))
```

## Array Mathematics

As such, it probably won’t surprise you that you can just use `+`, `-`, `*`, `/` or `%` to `add`, `subtract`, `multiply`, `divide` or calculate the `remainder` of two (or more) arrays. However, a big part of why NumPy is so handy, is because it also has functions to do this. The equivalent functions of the operations that you have seen just now are, respectively, `np.add()`, `np.subtract()`, `np.multiply()`, `np.divide()` and `np.remainder()`.

You can also easily do exponentiation and taking the square root of your arrays with `np.exp()` and `np.sqrt()`, or calculate the sines or cosines of your array with `np.sin()` and `np.cos()`. Lastly, its’ also useful to mention that there’s also a way for you to calculate the natural logarithm with `np.log()` or calculate the dot product by applying the `dot()` to your array.
Check out this small list of aggregate functions:
a.sum()|	Array-wise sum
a.min()|	Array-wise minimum value
b.max(axis=0)|	Maximum value of an array row
b.cumsum(axis=1)|	Cumulative sum of the elements
a.mean()|	Mean
b.median()	|Median
a.corrcoef()|	Correlation coefficient
np.std(b)	|Standard deviation

However, you can also compare entire arrays with each other! In this case, you use the `np.array_equal()` function. Just pass in the two arrays that you want to compare with each other and you’re done.
Note that, besides comparing, you can also perform logical operations on your arrays. You can start with `np.logical_or()`, `np.logical_not()` and `np.logical_and()`. This basically works like your typical `OR`, `NOT` and `AND` logical operations.

## Transpose of Arrays
```python
# Print `my_2d_array`
>>> print(my_2d_array)
array([[1 2 3 4]
       [5 6 7 8]])

# Transpose `my_2d_array`
>>> print(np.transpose(my_2d_array))
array([[1 5]
       [2 6]
       [3 7]
       [4 8]])
# Or use `T` to transpose `my_2d_array`
>>> print(my_2d_array.T)
array([[1 5]
       [2 6]
       [3 7]
       [4 8]])
```

## Misc 1
`ravel()` function allows you to flatten your arrays. This means that if you ever have 2D, 3D or n-D arrays, you can just use this function to flatten it all out to a 1-D array.
```python
>>> print(x1)
array([[ 1.  1.  1.  1.  1.  1.]
       [ 1.  1.  1.  1.  1.  1.]])

>>> print(x1.ravel())
array([ 1.  1.  1.  1.  1.  1.  1.  1.  1.  1.  1.  1.])
```
## Misc 2
`np.prod()` Returns the product of array elements over a given axis. 

```python
>>> np.prod([1.,2.])
2.0

>>> np.prod([[1.,2.],[3.,4.]])
24.0

>>> np.prod([[1.,2.],[3.,4.]], axis=1)
array([  2.,  12.])
```

## Misc 3
`np.random.shuffle()` Modify a sequence in-place by shuffling its contents.
```python
>>> arr = np.arange(10)
>>> np.random.shuffle(arr)
>>> arr
[1 7 5 2 9 4 3 6 0 8]

# Multi-dimensional arrays are only shuffled along the first axis:
>>> arr = np.arange(9).reshape((3, 3))
>>> np.random.shuffle(arr)
>>> arr
array([[3, 4, 5],
       [6, 7, 8],
       [0, 1, 2]])
```

## Help in Numpy
```python
# Look up info on `mean` with `np.lookfor()` 
>>> print(np.lookfor("mean"))

# Get info on data types with `np.info()`
>>> np.info(np.ndarray.dtype)
```


:trollface:
