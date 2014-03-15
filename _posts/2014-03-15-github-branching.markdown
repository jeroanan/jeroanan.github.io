---
layout: post
title:  "Trying Github Features: Branching"
date:   2014-03-15 21:00:00
categories: coding, Github
---

This week I've tried using a couple of features of Github that I'm new to: branching and issues. I've found them to be pretty useful additions to my development toolkit, and I'll continue to use them while developing <a href="https://github.com/jeroanan/Aquarius">Aquarius</a> in future. I will talk about branching in this post, and post about my experiences with issues in the next day or so.

First: branching. I've used branching in Subversion a lot in my day job, so it isn't an alien concept to me, but I'd never tried it with Github. I decided to give it a try a few days ago -- I wanted to make a big change to Aquarius that I wished to split over several nights/commits. I never commit when my unit tests are broken, so the software should (pretty much) always be committed in a working state. However, I didn't want to have a half-finished change in my Github repo for several days.

I had already begun work on my changes when branching occurred to me. I was worried that it was therefore too late to get this into a new branch, but as it turned out I can begin a new branch at any time and preserve the changes I have made:

{% highlight console %}
$ git checkout -b OpdsTemplating
{% endhighlight %}

This creates a new branch called "OpdsTemplating" and switches into it -- any changes I commit will now be to the "OpdsTemplating" branch until I switch out of it. I can list my branches and see which branch I'm currently in:

{% highlight console %}
$ git branch
* OpdsTemplating
  master
  sql-parameters
{% endhighlight %}

I have three branches here, and I'm currently using "OpdsTemplating", as denoted by the asterisk next to it. When I've done some work in my new branch and am ready to push to Github, I do it as normal, but with the branch name instead of "master":

{% highlight console %}
$ git push origin OpdsTemplating
{% endhighlight %}

Once I've finished working on the stuff I've made the branch for, it's time to merge. There are two options here: make Github do the merge for you or do it by hand in a console. Github provides very good documentation for doing it by hand. For me though, since Aquarius doesn't have any other contributors at the moment, I can make Github do it all automatically. This basically consists of the following steps:

1. Click to "view diffs and make pull request". This is prominently featured on the homepage of your repository's master branch when you've got another branch with commits against it.

2. Next you're taken to a page that shows the file differences between the master and sub branch. Once you've made sure that all is good, you can click on the button to make a pull request.

3. There will now be a pull request against your repository. Clicking to view it will show you details of the commits included and will feature a big green button that will allow you to merge in the pull request. Clicking that will do the merge and allow you to delete the sub branch if you want. 

Once that's all done, it's just a matter of switching back into a master and doing a pull on your local checkout:

{% highlight console %}
$ git checkout master
M	Config.py
Switched to branch 'master'
$ git pull
{% endhighlight %}

I'm very pleased to have found this method of keeping work-in-progress separate from the main branch. I will of course keep making most changes directly to master, but for those big, day-spanning changes, I can use branches and never again have to have nightmares about nasty things happening to ~/src/. 

Up next: issues management.

