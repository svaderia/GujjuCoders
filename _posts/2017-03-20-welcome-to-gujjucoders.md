---
layout: post
title: Welcome to GujjuCoders
author: sym
category: Blog
tags: [Jekyll]
---

Hello folks! Welcome to **GujjuCoders**.  
Initially I was thinking of writing a general welcome message for everyone out there. 
But then I realise that this is going to be almost our private blog.
So I'm going to write some general guidelines for you.  
I have spent enough time on desiging this blog you just need to know how Jekyll works and 
how you can write a post.  
## Resources  
First of all you should know about git and GitHub. Those who want to learn or refine their concept of git
here is the [resource.](https://www.git-tower.com/learn/git/ebook/en/command-line/introduction#start)
This [cheatSheet]({{ site.url }}{{ site.baseurl }}/assets/git-cheatsheet-EN-dark.pdf) comes handy while working with git.   
Now that you know about git, you need to learn Jekyll. Go through this 
[Tutorial](http://jekyll.tips/). If you get stuck anywhere 
this is the link to the official [documentation](https://jekyllrb.com/docs/home/).  
After gone through all this you should learn markdown and start writing blog. Megh is going to put one 
blog on markdown, if you are inpatient enough here is [link](http://www.markdowntutorial.com/). 
This [cheatSheet]({{ site.url }}{{ site.baseurl }}/assets/Markdown.pdf) can be very handy for Markdown.  
I'm going to explicitly tell you about How to write a post.  
## Writing post  
We are using a particular format for front-matter (You should know what front matter is)  
Here is a front matter of this blog.  
{% highlight ruby %}
layout: post
title: Welcome to GujjuCoders
author: sym
category: Blog
tags: [Jekyll]
{% endhighlight %}
See `_data` folder to know how author information looks like. Add the relevant details about yourself there.  
I have decided to make only two categories for blog now. `Blog` and `Notes`.
`Blog` will have your normal blog posts, whereas `Notes` will have some quick notes about any topic 
for your future reference.  
Only give relevant tags to your post. For multiple tag make an array of tags like  
`tags: [Python, Linux, Matlab]`   

## General structure 
You can use `_drafts` folder for your unfinished blog. Do read about it.  
Fork this repo and work on it locally than send a pull request. Don't commit unfinished work. You can use 
[stash](https://www.git-tower.com/learn/git/ebook/en/command-line/branching-merging/stashing#start) for this.  
Before you run it for first time install ruby, jekyll and its dependecies using following code.
{% highlight bash %}
sudo apt-get install ruby-full
sudo gem install jekyll
sudo gem install jekyll-paginate
sudo gem install pygments.rb
sudo gem install bundler
{% endhighlight %}

You can also view the site locally before sending the pull request.
Just run the following code in your terminal.
{% highlight bash %}
jekyll serve --config _config.yml,_config_dev.yml
{% endhighlight %}
If you planning to change some design do tell me before doing it.  
I'm expecting much from each and everyone. Let's share everything we know and learn a lot from this.
If you have any doubt contact me.  
Cheers!

