---
layout: post
title: Ubuntu configuration
author: sym
category: Blog
tags: [Linux]
image: /assets/linux.png
---

This post contains all the configuration changes made in my ubuntu system for
future reference. This is basically my personal Note, You can give some feedback and share your
changes as well. I will keep updating the list.  

## [VsCode](https://code.visualstudio.com/)
This is the editor in which I love to work nowadays. 
List of plugins added by me:
* Git History (git log)
* Java Debug
* Python
* C/C++
* MagicPythonp
* SpellChecker
* VSCode Great Icons
* Hopscotch (It's a color theme)

## Theme
Using `Unity tweak tool`  
Theme: `Paper`  
icons: `Paper`  
fonts: `deafult`

## TLP 
Installed it to decrease power consumption by ubuntu.

## Solved the issue of time conflict b/w two systems

## [youtube-dl](https://github.com/rg3/youtube-dl)
Probably the best software to download videos/audios from youtube.  
Bash script for extracting audio and save it to my Windows Music folder:
{% gist 60b10aafbd78db5219632a5df19f710e %}
Bash script for downloading Video and save it to my Windows Video folder:
{% gist 34778f781419ff6fe5e95e117a923092 %}

## [thefuck](https://github.com/nvbn/thefuck)
You should google to know about this beautiful fuck.

## zsh and [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

## [Powerlevel9K](https://github.com/bhilburn/powerlevel9k)
I :heart: the way my terminal is looking. :sunglasses:
{% highlight bash %}
POWERLEVEL9K_MODE='awesome-fontconfig'
POWERLEVEL9K_SHORTEN_DIR_LENGTH=2
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon dir vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status time)
POWERLEVEL9K_TIME_FORMAT="%D{\uf017  %H:%M \uf073  %d.%m.%y}"
POWERLEVEL9K_OS_ICON_BACKGROUND="black"
POWERLEVEL9K_OS_ICON_FOREGROUND="white"
POWERLEVEL9K_DIR_HOME_FOREGROUND="white"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_FOREGROUND="black"
POWERLEVEL9K_STATUS_VERBOSE=false
POWERLEVEL9K_DIR_DEFAULT_FOREGROUND="white"
ZSH_THEME="powerlevel9k/powerlevel9k"
{% endhighlight %}

## List of alias

{% highlight bash %}
alias download='./youtube.sh'
alias vdownload='./youtubev.sh'
alias c="reset"
alias kl="jekyll serve --config _config.yml,_config_dev.yml --drafts"
alias gl='git log --pretty=format:"%h : %an : %ar : %s/"'
{% endhighlight %}

