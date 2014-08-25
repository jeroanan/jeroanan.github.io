---
layout: post
title:  "Making Less of Aquarius"
date:   2014-08-26 09:00:00
categories: Aquarius
---

Because of some fairly big events in my personal life I've not kept up much with development on my main open source
project, <a href="https://github.com/jeroanan/Aquarius">Aquarius</a>. Coming back after a few months of relative
inactivity, I have been asking myself questions about the state that the project is now in and the directions I would
like to take it. 
 
Aquarius is supposed to be a lightweight ebook/<a href="http://opds-spec.org/">OPDS</a> web server. More and more I 
found myself adding support for new methods of persistence or front-ends. While this was a nice fun science project 
type approach to take, it really began to sap focus from the main objectives of the software. 
  
Aquarius will be a lightweight ebook server with an <a href="http://www.sqlite.org/">Sqlite</a> backend and an 
HTTP-based front end that serves either HTML or OPDS files depending on the type of application used to access it.

That's it. There will at this stage, for example, be no <a href="http://www.mongodb.org/">Mongo DB</a> back-end or 
desktop front-end. A lot of work has been done and will be done in Aquarius with regards to good software practices 
(namely <a href="http://en.wikipedia.org/wiki/SOLID_(object-oriented_design)">SOLID</a>) so that I can't change front
or back ends if something Really Horrible happens to Sqlite or HTTP. I do however aim to get rid of two headaches from
the project by doing this:
  
1. Feature creep around front and back ends detracting from the true aim of the software
2. The *pain* I have to endure when I want to add a feature to the back-end, which I then usually have to put into the
Mongo DB and hardcoded persistence modules.
    
To this end, several modules will be going bye-byes, if they haven't already:
 
1. Mongo DB persistence
2. Hardcoded persistence (no longer needed now sqlite persistence is working)
3. Hardcoded harvester (again, filesystem harvester works now so this isn't needed)
4. Console output (eugh)
   
On balance I still have lots of things I'd like to add to Aquarius, aside from what's already in the 
<a href="https://github.com/jeroanan/Aquarius/issues">Issues List</a>, including:

1. Support for .mobi files (in the issues list but worth a second mention!) -- I've had real issues finding a good 
library for this that will play nicely with Python 3. Watch this space for more of my trials and tribulations about 
this.

2. Some sort of integration with the catalog from <a href="http://www.gutenberg.org/">Project Gutenberg</a>: So when 
there's a search. Aquarius can say: "Hey, I found this stuff that also matches in PG's catalog)

3. More mash-up kind of stuff like this. I see some nicely done hooking up to other site's APIs and database as being
one of the main focuses of Aquarius development from here on.

In short, even though the Aquarius project might have seemed dormant for a little while now, it is by no means dead and
I still have lots of exciting plans for it. First though, to trim the fat...