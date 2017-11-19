---
title: The Decorator Design Pattern
date: 2017-11-18 18:20:00 -06:00
categories:
- design-patterns
---

The Decorator Pattern is a structural design pattern that has the ability to add behaviour to an existing class dynamically. 

We can use it to add additional features to objects without the need to heavily modify the underlying code using them.

This pattern avoids using inheritance to add functionality that is not required. It prevents us to break the [Open-Closed](http://deviq.com/open-closed-principle/) [SOLID Principle](http://deviq.com/solid/): *"An object or component should be open for extension but closed from modification"*. So, if we inherit from a class we have to modify that same class if we need more functionality, breaking this principle. When we use decorator, we extend that functionality to other classes.

So, ask your self: If I inherit from that class do I really need to pull in the entirety of that functionality or do I simply need to adjust the behaviour of one or two methods? If that is the case then maybe you can refer to the Decorator Pattern.

Here's an example on PHP:

