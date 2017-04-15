---
layout: post
title: Format() in Python
author: sym
category: Blog
tags: [Python]
---

Today I'm going to write about formatting of strings in Python using `format()` function. 
Sending out a root mail(in BITS) got me inspired to write an article on it. So here's something for my (and maybe even for your :wink:) future reference.
## Basic formatting
{% highlight python %}
' {} {}'.format('one', 'two')
' {} {}'.format(1, 2)
{% endhighlight %}
**Output**  
{% highlight bash %}
$ one two
$ 1 2
{% endhighlight %}

You can give placeholders an explicit positional index.
{% highlight python %}
' {1} {0}'.format('one', 'two')
{% endhighlight %}
**Output**  
{% highlight bash %}
$ two one
{% endhighlight %}

## Value conversion
The new-style simple formatter calls by default the `__format__()` 
method of an object for its representation. 
If you just want to render the output of str(...) 
or repr(...) you can use the `!s` or `!r` conversion flags.  
**Setup**
{% highlight python %}
class Data(object):

    def __str__(self):
        return 'str'

    def __repr__(self):
        return 'repr'
    def __format__(self):
        return 'format'
{% endhighlight %}
**Input**
{% highlight python %}
' {0!s} {0!r} {}'.format(Data())
{% endhighlight %}
**Output**
{% highlight bash %}
$ str repr format
{% endhighlight %}

## Padding and aligning strings
By default values are formatted to take up only as 
many characters as needed to represent the content. 
It is however also possible to define that a value 
should be padded to a specific length.
Default alignment is left.

{% highlight python %}
' {:10}!'.format('test')
' {:>10}!'.format('test')
{% endhighlight %}
**Output**
{% highlight bash %}
$       test!
$ test      !
{% endhighlight %}

By default string is being padded by space. 
But you can choose the padding character.
{% highlight python %}
' {:!<10}'.format('test')
{% endhighlight %}
**Output**
{% highlight bash %}
$ test!!!!!!
{% endhighlight %}
You can align in center as well
{% highlight python %}
' {:^10}!'.format('test')
{% endhighlight %}
**Output**
{% highlight bash %}
$    test   !
{% endhighlight %}
When using center alignment where the length of the 
string leads to an uneven split of the padding 
characters the extra character will be placed on the 
right side.
{% highlight python %}
' {:^6}!'.format('zip')
{% endhighlight %}
**Output**
{% highlight bash %}
$  zip  !
{% endhighlight %}

## Truncating long strings
Inverse to padding it is also possible to truncate overly long values to a specific number of characters.  
{% highlight python %}
' {:.5}'.format('shyamal')
{% endhighlight %}
**Output**
{% highlight bash %}
$ shyam
{% endhighlight %}

## Combining truncating and padding
It is possible to combine truncating and padding.
{% highlight python %}
' {:10.5}!'.format('shyamal')
{% endhighlight %}
**Output**
{% highlight bash %}
$ shyam     !
{% endhighlight %}

## Numbers
It is possible to do padding with numbers.
{% highlight python %}
' {:4d}'.format(42)
{% endhighlight %}
**Output**
{% highlight bash %}
$   42
{% endhighlight %}
Again similar to truncating strings the precision for floating point numbers limits the number of positions after the decimal point.

For floating points the padding value represents the length of the complete output. In the example below we want our output to have at least 6 characters with 2 after the decimal point.
{% highlight python %}
' {:06.2f}'.format(3.141592653589793)
{% endhighlight %}
**Output**
{% highlight bash %}
$ 0034.14
{% endhighlight %}

## Named placeholders

**Setup**
{% highlight python %}
data = {'first': 'Shyamal', 'last': 'Vaderia'}
{% endhighlight %}
**Input**
{% highlight python %}
' {last} {first}'.format(**data)
{% endhighlight %}
**Output**
{% highlight bash %}
$ Vaderia Shyamal
{% endhighlight %}
.format() also accepts keyword arguments.
{% highlight python %}
' {first} {last}'.format(first='Jon', last='Snow!')
{% endhighlight %}
**Output**
{% highlight bash %}
$ Jon Snow!
{% endhighlight %}

## Getitem and Getattr

New style formatting allows even greater flexibility in accessing nested data structures.

It supports accessing containers that support `__getitem__` like for example dictionaries and lists:  
**Setup**
{% highlight python %}
person = {'first': 'Jean-Luc', 'last': 'Picard'}
data = [4, 8, 15, 16, 23, 42]
{% endhighlight %}
**Input**
{% highlight python %}
' {p[last]} {p[first]}'.format(p=person)
' {d[4]} {d[5]}'.format(d=data)
{% endhighlight %}
**Output**
{% highlight bash %}
$ Picard Jean-Luc
$ 23 42
{% endhighlight %}

**Setup**
{% highlight python %}
class Plant(object):
    type = 'tree'
    kinds = [{'name': 'oak', 'size': 'big'}, {'name': 'maple', 'size': 'small'}]
{% endhighlight %}
**Input**
{% highlight python %}
' {p.type}: {p.kinds[0][name]}'.format(p=Plant())
{% endhighlight %}
**Output**
{% highlight bash %}
$ tree: oak
{% endhighlight %}

## Datetime

**Setup**
{% highlight python %}
from datetime import datetime
{% endhighlight %}
**Input**
{% highlight python %}
' {:%Y-%m-%d %H:%M}'.format(datetime(2001, 2, 3, 4, 5))
{% endhighlight %}
**Output**
{% highlight bash %}
$ 2001-02-03 04:05
{% endhighlight %}

## Parametrized formats

{% highlight python %}
' {:.{prec}} = {:.{prec}f}'.format('Gibberish', 2.7182, prec=3)
{% endhighlight %}
**Output**
{% highlight bash %}
$ Gib = 2.718
{% endhighlight %}

{% highlight python %}
' {:{width}.{prec}f}'.format(2.7182, width=5, prec=2)
{% endhighlight %}
**Output**
{% highlight bash %}
$  2.72
{% endhighlight %}

{% highlight python %}
' {:{prec}} = {:{prec}}'.format('Gibberish', 2.7182, prec='.3')
{% endhighlight %}
**Output**
{% highlight bash %}
$ Gib = 2.72
{% endhighlight %}

**Setup**
{% highlight python %}
from datetime import datetime
dt = datetime(2001, 2, 3, 4, 5)
{% endhighlight %}
**Input**
{% highlight python %}
' {:{dfmt} {tfmt}}'.format(dt, dfmt='%Y-%m-%d', tfmt='%H:%M')
{% endhighlight %}
**Output**
{% highlight bash %}
$ 2001-02-03 04:05
{% endhighlight %}

## Custom objects
The datetime example works through the use of the `__format__()` magic method. You can define custom format handling in your own objects by overriding this method. This gives you complete control over the format syntax used.

**Setup**
{% highlight python %}
class HAL9000(object):

    def __format__(self, format):
        if (format == 'open-the-pod-bay-doors'):
            return "I'm afraid I can't do that."
        return 'HAL 9000'
{% endhighlight %}
**Input**
{% highlight python %}
' {:open-the-pod-bay-doors}'.format(HAL9000())
{% endhighlight %}
**Output**
{% highlight bash %}
$ I'm afraid I can't do that.
{% endhighlight %}

