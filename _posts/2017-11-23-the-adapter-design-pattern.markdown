---
title: The Adapter Design Pattern
date: 2017-11-23 19:49:00 -06:00
categories:
- design-patterns
tags:
- design patterns
- php
---

We all use adapters in our daily life, when we want to connect a DVI monitor to a VGA port we need an adapter to do that, or when we want to use a microSD in a SD memory card. So guess what, we can do kind of the same thing using this design pattern.

An **adapter** allows you to translate one interface for use with another. Adapters basically allow objects to work together in a situation where they couldn't because of their different and incompatible interfaces. The adapter translates the calls to its interface into calls that the original interface understands. 

To explain it a little bit better there's nothing like see it in action with an example. We're going to use PHP, but the same principles apply to any other language.

So imagine that someone gives you an old school Walkman, but you're a teenager that only knows how to use an iPod and *touch* buttons on the screen, so we're going to create an adapter for you, so you don't have to worry about how it works, you just *touch* on our *Walkman Adapter* and it does the job.

1. First lets define our **Walkman** *Class* and *Interface*, so to keep it simple it just implements the `pressPlay()` function to start listening to music:

```php
interface WalkmanInterface {

    public function pressPlay();

}

class Walkman implements WalkmanInterface{
    
    public function pressPlay(){

        echo "Playing some music on the Walkman...";

    }

}
```

2. Next we're going to take care of the **iPod** *Class* and *Interface* which implements the `touchPlay()` function to start listening music on the iPod:

```php
interface iPodInterface {

    public function touchPlay();

}

class iPod implements iPodInterface{

    public function touchPlay(){

        echo "Playing some music on the iPod...";

    }

}
```

3. Now lets define our **WalkmanAdapter** *Class*. It must implement the *Interface* that we're currently using, in our case the *iPodInterface* and it must accept an *instance* of our *Walkman Class* on it's *constructor*. Remember we've to [program to an interface, not an implementation](https://www.codeproject.com/Articles/702246/Program-to-Interface-not-Implementation-Beginners). Watch how the `touchPlay()` function is *translated* into a `pressPlay()` Walkman function:

```php
class WalkmanAdapter implements iPodInterface {

    private $walkman;

    public function __construct(WalkmanInterface $walkman){

        $this->walkman = $walkman;

    }

    public function touchPlay(){

        $this->walkman->pressPlay();

    }

}
```

4. Finally lets just create a sample **Person** *Class* that will just *listen* to music on a specific device:

```php
class Person {

    public function listen(iPodInterface $ipod){

        $ipod->touchPlay();

    }

}
```

5. Now to test it out lets just tell our person to listen to music on the Walkman using the *Walkman Adapter* by creating a new instance of *WalkmanAdapter* and passing out an instance of *Walkman*, so the adpater will take care of *translating* the *touch* action into a *press* action:

```php
$person = new Person;

$person->listen(new WalkmanAdapter(new Walkman));
```

And the output will be:

```
Playing some music on the Walkman...
```

You can run and view the full code here: [codepad.org/vduny4f4](http://codepad.org/vduny4f4)

And that's all! Painless code right?