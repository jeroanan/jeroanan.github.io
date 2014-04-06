---
layout: post
title:  Separating Business Rules from Data Access in Aquarius
date:   2014-04-06 21:00:00
categories: coding, Aquarius
comments: true
---

Last week I was looking through Aquarius's data access code. I wanted to play with <a href="http://www.mongodb.com/">MongoDB</a>, and I thought that adding a new type of persistence would be the perfect opportunity to work with NoSQL while comparing it with sqlite.

Unfortunately I didn't have to dig very deep to find that this wouldn't be a simple new persistence type matter:

{% highlight python %}
class AddBook(object):

    def __init__(self, connection):
        self.__connection = connection

    def add_book(self, book):
        book_id = GetExistingBookId(self.__connection).get_existing_book_id(book)
        if book_id == -1:
            book.id = self.__add_new_book_returning_its_id(book)
        else:
            book.id = book_id
        self.__add_book_formats(book)

	  def __add_new_book_returning_its_id(self, book):
        [data access]

    def __add_book_formats(self, book):
	 	  [data access]

	 [...more data access functions...]
{% endhighlight %}

Yuck! This is bad for a couple of reasons, but for me the root of it is that the business logic (all of the add\_book method) and the details of data access (pretty much the rest of the class) are lumped together. If I wanted to add a new persistence type for MongoDB I'd have to replicate that high-level business logic in there as well, and again for each different persistor. I'd also argue that the diverse data access methods in this class violate <a href="http://en.wikipedia.org/wiki/Single_responsibility_principle" title="Single Repsonsibility Principle">SRP</a>, but that is secondary to what I'm talking about here.

How did this class get like this? Well, I guess I kind of sleptwalked into it. I'm learning and honing my craft all the time, and this is an example of coming back to a piece of code months later to find it's not what you'd write now.

Anyway, things can't remain like this; the lack of a good definition of business rules is to me a bit of a flaw in Aquarius's design and I really want to play with MongoDB. So, I've started a new branch called "BusinessSeparation". My plan is to have a new module called "interactors" that contain the business rules. For instance I have already committed a first go at "AddBookInteractor.py":

{% highlight python %}

class AddBookInteractor(object):
    def __init__(self, persistence):
        self.__persistence = persistence

    def execute(self, book):
        b = self.__persistence.get_book_by_title_and_author(book)
        if b.id == "":
            self.__persistence.add_book(book)
{% endhighlight %}

...I plan to rinse and repeat for the other use cases in Aquarius, so for the time being, Aquarius.py calls into the interactors instead of the persistence.