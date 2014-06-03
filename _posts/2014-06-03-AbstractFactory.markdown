---
layout: post
title:  Abstract Factory
date:   2014-06-03 21:00:00
categories: coding patterns
comments:   true
---

The first pattern I'd like to cover is the 
<a href="http://en.wikipedia.org/wiki/Abstract_factory_pattern">Abstract Factory</a>. Its intent is to abstract away
the creation of families of related objects. 

When implemented, the Abstract Factory pattern consists of the following:

1. An interface/abstract class for the factory
2. An interface/abstract class for each type of object (or product) that the factory is to construct
3. Concrete implementations of the different factories
4. Concrete implementations of the various products

Let's start with our factory interface:

{% highlight java %}
public interface ClothesFactory {
    Shirt GetShirt();
    Trousers GetTrousers();
}
{% endhighlight %}

...Like any interface, it just defines the operations that the concrete classes must implement. Our factories will
provide operations that return some kind of Shirt and some kind of Trousers. Shirt and Trousers are also interfaces:
 
 {% highlight java %}
 public interface Shirt {
 }
 
 public interface Trousers {
 }
 {% endhighlight %}
 
 I could of course define any sort of operation that I'd want my concrete Shirt and Trousers to implement. For
 this example I'm only implementing toString() though.
 
 Let's have a look at our concrete factories:
 
 {% highlight java %} 
 public class SmartClothesFactory implements ClothesFactory {
     @Override
     public Shirt GetShirt() {
         return new SmartShirt();
     }
 
     @Override
     public Trousers GetTrousers() {
         return new SmartTrousers();
     }
 }
 
 public class SummerClothesFactory implements ClothesFactory {
     @Override
     public Shirt GetShirt() {
         return new TShirt();
     }
 
     @Override
     public Trousers GetTrousers() {
         return new Shorts();
     }
 }
 {% endhighlight %}
 
 ...Depending on how we want to dress, we can use the SmartClothesFactory or the SummerClothesFactory. This demonstrates
 the most important aspect of the Abstract Factory pattern, along with the abstraction away of object creation: The
 objects made available for creation by each factory are related. There's no chance anyone using our SmartClothesFactory
 would turn up to the dinner party in a pair of shorts!
 
 Finally, let's have a look at one of the concrete clothes classes:
 
 {% highlight java %}
 public class SmartTrousers implements Trousers { 
     @Override
     public String toString() {
         return "A pair of smart trousers";
     }
 }
 {% endhighlight %}
 
 There are a bunch of other similar concrete clothes classes that do the same sort of thing. The code for my abstract
  factory implementation can be found on my 
  <a href="https://github.com/jeroanan/Patterns/tree/master/AbstractFactory/src/com/patterns/abstractfactory">Github</a>.
  
  Next, I will be learning more about the <a href="http://en.wikipedia.org/wiki/Builder_pattern">Builder pattern</a>.
  Stay tuned!