---
layout: post
title: The World of Real Time
author: mgh_tkr
tags: [Technology, Web_D]
image : /assets/nodejs.png

---

Well, let me first introduce you to a term which is pretty rare for the general public, **[Web 2.0](https://en.wikipedia.org/wiki/Web_2.0)**. Web 2.0 refers to the collection of websites that focus on users, their interaction to the web application, utilising user-content and providing easy to use interfaces. The most "popular" web apllications falling under this domain are social media applications. Most of these websites use technologies that require updates in the real time, the best example of which are chat applications and the forerunner in real-time web based frameworks is Express.js, a framework of Node.js.  

**What is [Node.js](https://en.wikipedia.org/wiki/Node.js)?**  

Chrome, one of the fastest web browsers, uses a compiler(yes, even they need to convert code to machine language) known as V8, for compiling JavaScript code. Node.js is a _run-time environment_ that is built on this V8 engine. This simply means you can run JavaScript codes just like another programming language as C or python on your system.  

**Why Node.js for real-time?**  

It has hardly been 5 months since I got into back-end web development. Though I still work in [Django](https://en.wikipedia.org/wiki/Django_(web_framework)), a Python framework for server-side code, I was very curious on trying Node.js and specifically Express.js, tempting me to take-up a course for Web Development at my institute. That course was enough to indulge me in the world of JavaScript. Though the logics were totally similar to any other programming language, understanding concepts like closure and callbacks(explained further) was very intriguing. Though I had used **Higher-Order Functions** while learning python, JavaScript opened doors for many newer concepts. This is definitely not a comparison between Python and JS or even Django to Express. They are not comparable, apples and oranges!. Their usage depends totally on the aim of your project. Django, with its tons of packages written in Python is easier to implement for beginners as well as forces more structured code than Node. On the other hand, Node is almost ten times faster launch time when compared to Django based web applications : see, their usage depends on the purpose.  

The main idea behind Node.js is using non-blocking, event driven I/O.  Most languages use synchronous web service, meaning whenever a client sends a request, all other activities are blocked until a response is provided whereas Node.JS uses asynchronous web services, that enables it to handle thousands of requests at a time. Using it for heavy purposes is definitely not recommended but when it comes to building network applications that require faster request/response handling, it is probably the best in the business.  

**Understanding the Event Loop**  

Traiditional web services work in a way in which each new request leads to the generation of a new thread, a new pathway for communication with the server which takes up system RAM. Consider a simple calculation. If each thread has a memory of 2 MB associated with it and it runs on a system of 8 GB RAM, a theoretical maximum of 4000 simultaneous connections is possible. Node.js rather operates on a single-thread, using non-blocking I/O calls using callbacks, in an event loop that facilitates responding to requests as a whole once they have been processed, that enable it to deal with a theoretical maximum of 1M concurrent connections.  

![webservices](/assets/eventloop.png)

_Credits for calculations and Image : Tomislav Capan, JS Developer@[TOPTAL](https://www.toptal.com/nodejs/why-the-hell-would-i-use-node-js)_  

Getting back to Synchronized and Asynchronized programming. Node.js is single threaded : one command at a time. This is when the event loop comes into picture. Asynchronous portion of the code is the one which we don't necessarily want to be executed right now but at some "later" point of time, decided by the calling function. The code is passed as a function to the calling function and it is "called back" once required. All this while, when the code is being processed, the primary application is running normally. These functions that are to be called back are stored in a place known as an **Event Loop** and are executed once the memory stack becomes empty.  

Consider a very simple example. In a restaurant, there is only one person to serve food(a single thread) and a single chef(server/database). The restaurant serves only one food item that takes, say 5 seconds to prepare. The time to get the request from the customer and take it to the chef as well as transferring the finished item from the chef to the customer is very fast compared to this(a normal console.log takes 2-3 ms).  

For a normal Synchronized thread, if three customers line up, the process would be : A customer gives the order and the waiter takes it to the chef. The waiter waits for 5 seconds and returns with the order to the customers while the other two wait.  

As JS code, if we print "Order taken", "Order completed" and "Order received by the customer", the process would be like:

```javascript

console.log("Order of Customer 1 taken");
console.log("Order taken to the chef");
console.log("Order received by customer 1");

console.log("Order of Customer 2 taken");
console.log("Order taken to the chef");
console.log("Order received by customer 2");

console.log("Order of Customer 3 taken");
console.log("Order taken to the chef");
console.log("Order received by customer 3");

```

Node.js would execute the process in the most logically efficient way. The waiter takes the order and provides it to the chef. While the chef prepares the order, it goes and takes another order and gives it to the chef and similarly for the third customer. Once the orders are ready, it gives them to the customers, one by one, a process that takes around 4-6 ms(less in many cases). Hence all the customers got the order in 5 seconds only.  

As we don't have a server for handling requests, we can depict this by using a setTimeout() function, which takes a "callback" function and a time value as its attributes, callback : the function to be executed in the set time.

```javascript
console.log("Order of 1 taken");
setTimeout(callback,5000);

console.log("Order of 2 taken");
setTimeout(callback,5000);

console.log("Order of 3 taken");
setTimeout(callback,5000);

function callback(){
	console.log("Made and delivered.");
}
```

Output :
{% highlight ruby %}
Order of 1 taken  
Order of 2 taken  
Order of 3 taken  
Made and delivered. #for 1
Made and delivered. #for 2
Made and delivered. #for 3
{% endhighlight %}  

In the process, first Order of 1 taken is printed. setTimeout shifts the callback function to the Eventloop after processing it, during which it makes room for the next line of synchronous code i.e. console.log(#2) to get executed. As the timer for 5 seconds comes to an end, and the primary stack is empty, the callbacks queued up in the event loop are executed one after the other in the form of responses. Do check the video [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=31s)

Clearly this is the superpower of JS.  

**How servers handle requests in real time?**  

I thought of including a basic overview of how websockets function too. I won't be going in much detail but whenever a normal http request is made, the connection between the server and the client is broken after the necessary response. This is when sockets come into play. Every connection has two sockets, one on the client side, signified by the IP address of the client and a randomly generated port by the server. The other socket is at the server side, consisting of its domain name(IP address actually) and a fixed port(80 in almost all the cases). The sockets maintain a continuous connection between the client and the server until either one of them breaks it. This connection facilitates data transfer at all points till the connection exists. The client has a random port as the connection being temporary, the port can be re-used by the server for other clients too.  

**Now for the "Survival Tactics :P".**

I am still doing development and Django and would be continuing in it. Trying out Node.js and well, JS for the very first time was just to cater to my "strong desires" for testing out this awesome functionality. For newwer developers, I'd suggest to start with Django itself. Its cleaner infrastructure would help to understand how requests work and the response is rendered. Later on, if you wish to shift to Node.js, it will be easier to grasp the methods by which it functions. This was just an overview over why Node.js is becoming popular in handling massive requests for real-time based chat applications. Do give it a try as it never fails to amaze.
