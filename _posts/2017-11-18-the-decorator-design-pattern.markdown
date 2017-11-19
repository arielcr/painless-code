---
title: The Decorator Design Pattern
date: 2017-11-18 18:20:00 -06:00
categories:
- design-patterns
tags:
- design patterns
- php
---

The Decorator Pattern is a [structural design pattern](https://www.javatpoint.com/structural-design-patterns) that has the ability to add behaviour to an existing class dynamically.

We can use it to add additional features to objects without the need to heavily modify the underlying code using them.

This pattern avoids using inheritance to add functionality that is not required. It prevents us to break the [Open-Closed](http://deviq.com/open-closed-principle/) [SOLID Principle](http://deviq.com/solid/): *"An object or component should be open for extension but closed from modification"*. So, if we inherit from a class that we need to modify it several times to add functionality, then we're breaking this principle. When we use decorator, we extend that functionality to other classes.

So, ask your self: *If I inherit from that class do I really need to pull in the entirety of that functionality or do I simply need to adjust the behaviour of one or two methods?* If that is the case then maybe you can refer to the **Decorator Pattern**.

So here's the pattern explained on PHP. We're going to use a *Coffee Service* implementation example, where you can order a single coffee and you also have the option to add milk, cinnamon or both, then we can get the final cost and description. The idea is that we can understand this pattern by using the analogy of *decorating* the coffee.

1. First we need an [interface](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html), this is important because every Decorator Class needs to implement the same interface as the core class:

```php
interface CoffeeService {

    public function getCost();

    public function getDescription();

}
```

2. We create the basic class, in our case is the `SingleCoffee Class`:

```php
class SingleCoffee implements CoffeeService{

    public function getCost(){
        return 15;
    }

    public function getDescription(){
        return 'Single Coffee';
    }

}
```

3. Then we create our first Decorator, it must implement the same interface as the SingleCoffee Class, and the constructor must accept an instance or implementation of the same contract:

```php
class Milk implements CoffeeService {

    protected $coffeeService;

    function __construct(CoffeeService $coffeeService){
        $this->coffeeService = $coffeeService;
    }

    public function getCost(){
        return 5 + $this->coffeeService->getCost();
    }

    public function getDescription(){
        return $this->coffeeService->getDescription() . ', with milk';
    }

}
```

4. We create our final decorator class:

```php
class Cinnamon implements CoffeeService {
    
    protected $coffeeService;

    function __construct(CoffeeService $carService){
        $this->coffeeService = $coffeeService;
    }

    public function getCost(){
        return 2 + $this->coffeeService->getCost();
    }

    public function getDescription(){
        return $this->coffeeService->getDescription() . ', with cinammon';
    }

}
```

Finally, to run our code with create an instance of our basic class and wrap it with the decorators that we want:

```php
$coffeeService = new Cinnamon(new Milk(new SingleCoffee));

echo $coffeeService->getCost();

echo $coffeeService->getDescription();

```

The output of this would be:

```
22 Single Coffee, with milk, with cinammon%
```