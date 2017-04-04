---
layout: post
title: The Batman Curve
subtitle: What if Bruce Wayne was a coder?
author: mdp98
category: Blog
tags: MATLAB
---

Just admit it! Everyone loves Batman. And if you don't, are you even human bruh? Okay, done with the jokes. Time to get a little geeky about this DC superhero. If you are a man of Science, you would definitely agree that every shape in this physical world is a representation of some complex mathematical equations. So, I won't be lying if I say that if I somehow know the mathematical equation of some shape, I can recreate it.

Let us create the famous Batman logo.

MATLAB is a powerful tool to plot mathematical equations, which are otherwise tiresome to solve. The MATLAB code to plot the Batman curve is as follows:

```MATLAB
%Initialization : Clearing workspace
clf; clear all;

syms x y      % Specifies that x and y are variables and the equations would be in their terms

%Equations defining the curve
eq1 = ((x/7)^2*sqrt(abs(abs(x)-3)/(abs(x)-3))+(y/3)^2*sqrt(abs(y+3/7*sqrt(33))/(y+3/7*sqrt(33)))-1);
eq2 = (abs(x/2)-((3*sqrt(33)-7)/112)*x^2-3+sqrt(1-(abs(abs(x)-2)-1)^2)-y);
eq3 = (9*sqrt(abs((abs(x)-1)*(abs(x)-.75))/((1-abs(x))*(abs(x)-.75)))-8*abs(x)-y);
eq4 = (3*abs(x)+.75*sqrt(abs((abs(x)-.75)*(abs(x)-.5))/((.75-abs(x))*(abs(x)-.5)))-y);
eq5 = (2.25*sqrt(abs((x-.5)*(x+.5))/((.5-x)*(.5+x)))-y);
eq6 = (6*sqrt(10)/7+(1.5-.5*abs(x))*sqrt(abs(abs(x)-1)/(abs(x)-1))-(6*sqrt(10)/14)*sqrt(4-(abs(x)-1)^2)-y);

% Transcendental equation 
eqf = '((x/7)^2*sqrt(abs(abs(x)-3)/(abs(x)-3))+(y/3)^2*sqrt(abs(y+(3*sqrt(33))/7)/(y+(3*sqrt(33))/7))-1)*(abs(x/2)-((3*sqrt(33)-7)/112)*x^2-3+sqrt(1-(abs(abs(x)-2)-1)^2)-y)*(9*sqrt(abs((abs(x)-1)*(abs(x)-3/4))/((1-abs(x))*(abs(x)-3/4)))-8*abs(x)-y)*(3*abs(x)+3/4*sqrt(abs((abs(x)-3/4)*(abs(x)-1/2))/((3/4-abs(x))*(abs(x)-1/2)))-y)*(9/4*sqrt(abs((x-1/2)*(x + 1/2))/((1/2-x)*(1/2+x)))-y)*((6*sqrt(10))/7+(3/2-abs(x)/2)*sqrt(abs(abs(x)-1)/(abs(x)-1))-(6*sqrt(10))/14*sqrt(4-(abs(x)-1)^2)-y)=0';

axes('Xlim', [-7.25 7.25], 'Ylim', [-5 5]);       %Sets limit of x and y axes
hold on                                           %Plots following equations on same plot

%Plotting equations
ezplot(eq1,[-8 8 -3*sqrt(33)/7 6-4*sqrt(33)/7]);
ezplot(eq2,[-4 4]);
ezplot(eq3,[-1 -0.75 -5 5]);
ezplot(eq3,[0.75 1 -5 5]);
ezplot(eq4,[-0.75 0.75 2.25 5]);
ezplot(eq5,[-0.5 0.5 -5 5]);
ezplot(eq6,[-3 -1 -5 5]);
ezplot(eq6,[1 3 -5 5]);

title('Batman');                                  %Defines plot title
xlabel('');                                     
ylabel('');
hold off                                          %All equations before this are plotted on same plot

figure                                            %Opens empty figure
axes('Xlim', [-7.25 7.25], 'Ylim', [-5 5]);       %Sets limit of x and y axes
hold on
ezplot(eqf, [-7 7 -3 3]);                         %Removes the additional disturbance and plots a clean figure
hold off
```

The result looks something like this.

![Batman_curve_matlab](https://lh3.googleusercontent.com/-SEYMteABx9w/WKgSQucC0RI/AAAAAAAAEE8/6BOmGea2n7kZFjBQvZ26o-w-eLOqmAjkwCLcB/s1600/batman.jpg)

Go ahead! Try it.
In case of some error or query, feel free to ask.
