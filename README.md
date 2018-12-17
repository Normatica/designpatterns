# Desing Patterns made easy  
This is an example of some of the most important desing patterns used in software development, implemented in Java and with every explanaition needed to understand it's use.  

## Factory Design Pattern  
#### What is it used for?  
The Factory is a creational pattern, which means that is used for creating/instantiating objects. There'll be many cases where you'll have some kind of superclass or interface and a lot of subclasses extending or implementing it. Commonly, each of those subclasses have their own constructors, and the way to instantiate them is calling that subclass' constructor directly. The idea of the Factory pattern is using a common Factory method to instantiate every single type of object whose class descend directly from another superclass/interface, instead of having isolated constructors. Let's see an example:  

Let's say that we are creating an application for a fruit store. Every single fruit regardless which fruit it is, can me sold. Okey so now, we can actually start thinking of a Fruit superclass, or even a Fruit Interface, both allowing us to define the common method sell() that all the fruits should have. Let's write that:  
```
public interface Fruit{  
  public void sell();  
}  
```  
I'm creating an interface here, as it's quicker and perfectly valid for the explanation. Going back to our example, let's create three kinds of fruit for the porpouse of the application:  
```
public class Apple implements Fruit{  
  public void sell(){  
    System.out.println("We've just sold a red apple!");  
  }  
}  
  
public class Banana implements Fruit{  
  public void sell(){  
    System.out.println("We've just sold a yellow banana!");  
  }  
}  
  
public class Pear implements Fruit{  
  public void sell(){  
    System.out.println("We've just sold a pretty good looking pear!");  
  }  
}  
```  
Now that we have all our fruits created, it's when the Factory Pattern comes in hand. Without using it, on our code we would probably have a bunch of conditions depending on which type of fruit we would like to instantiate. The next peace of code, could be an example of what I have just said:  
```
if(color == "red"){
  Fruit apple = new Apple();
} else if (color == "yellow"){
  Fruit banana = new Banana();
} else if(color == "green"){
  Fruit pear = new Pear();
} else {
  System.err.println("No matching fruit.");
}
```   
Pretty messy, isn't it? Why would you have to check a conditions every time you'd like to instantiate an object? The answer is: You don't have to, because we know about Software Engineering so we could apply a Factory pattern! Lets see, instead of creating the objects in our code always checking for a contition manually, we could just create a class that does that for us! Note that mostly every time you see a Factory Pattern implemented, it will have is own class with 'Factory' in it's name. Let's get down to work, we are going to create a FruitFactory class, with a method getFruit() on it. Lets also make that method static, because there's not need of instantiating the Factory class (why would we?) and of course, that method needs a parameter: a criteria. Depeding on the value of that criteria, we will create a different object. Here is an example:  
```
public class FruitFactory {
  public static Fruit getFruit(String criteria) {
    if(criteria == "red") return new Apple();
    else if (criteria == "yellow") return new Banana();
    else if (criteria == "green") return new Pear();
    else return null;
  }
}
```  
##### Note that the method returns a Fruit object, we are not specifing any subclass type.  
Now our pattern is gaining some shape. We've defined a common Factory class that creates every type of fruit in our application, so we won't have to worry about our objects conditions anymore. Now, instead of checking for the criteria in our code continually, we can just call the getFruit() method and pass the criteria.  
```
Fruit pear = FruitFactory.getFruit("green");
```  
Easy as that! We can summarize what we've learned about the Factory pattern:  
- It's very usefull when you cannot know what type of object you're going to instantiate.  
- The subclasses are the ones which specify the objects.  
- It's quicker than checking for a condition every time you want to create an object.  
- You pass the responsability of choosing the object type to the Factory class.  
  
## Next: Singleton Pattern! Coming soon...
