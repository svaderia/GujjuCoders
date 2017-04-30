---
layout: post
title: Dont "gcc" Everytime
author: sam
category: Blog
tags: [gcc,C]
---

So, How many of you code in **C**? Raise your hand.  
Keep it down, you look like an idiot raising your hand alone in a room `#foreverAlone`. 
Now I am telling you a trick that will make your life easy. _Atleast coding in C easy_.
### WHY
 So why do we need something if we have got our beloved gcc??  
 Well for starters we need to type in same command multiple times when we debug. This is easy if we have one file to compile but once you start using header files and multiple C files this is hectic and scopes of error increases. This doesn't end. What if your code is 1000's of lines and one file takes tangible time to compile do you want to wait for minutes for code to compile which you havent even changed just so you can debug a silly mistake. All this and more is overcome by `makefile`, after which you just have to input `make` in the terminal and lo! file is compiled.  
### CODE  
 So make a "makefile" named file in the directory where your C files are present. Then comes the command in the "makefile".  
{% highlight bash %}
CC = gcc
CFLAGS =-g -I .
DEPS = myheader.h
OBJ = mydriver.o myheader.o

%.o: %.c $(DEPS)
	$(CC) -c $^ $(CFLAGS)

myexe: $(OBJ)
	gcc -o $@ $^ $(DEPS) $(CFLAGS)

clean:
	$(RM) myexe
{% endhighlight %}
I have no intention of speeding past this.So now comes the explanation.  
### MACROS  
 **CC** tells the C compiler name to make file.  
 **CFLAGS** adds any flag you want to add to the compilation. In this case it lets compiler know that required header file is in the same directory.  
 **DEPS** this macro is used by us to give all the dependecies. All the include files should be part of this Macro.  
 **OBJ** this are the objects of interests i.e. the object files. All the object files should be a part of this Macro.  

### COMMAND  
 This is of type  
 > _left argument_ **:** _right argument_  
 >**tab_space** _thecommand_  
 
 **left argument** is the name of the command while  
 **right argument** is the dependencies needed for the command.  
 **thecommand** gives the Actual Command to the bash i.e. terminal.  
 **$( )** this is to use any defined macro in command.  
 **$@** this is shortcut for left arguments of :  
 **$^** this is shortcut for right argument of :  
### BEHIND THE SCENES
 * In the first command we are making object files from all the C files once we update any dependecy i.e. include files in this command. This doesn't execute for specific C file unless any include file or the C file is changed after the last make.
 * In the second command we are using all object files as dependecies so whenever even 1 object file changes only then remake the executable file.  
 