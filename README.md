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
  
## Singleton Design Pattern  
This is a pretty interesting one, it may look easy at first, but this pattern has to be used in a very restrictive situation. First of all and as his name describes, the Singleton Pattern tells that any class affected by it can only have one instance at the same time. It's own definition is as simple as that, you cannot have 2 or more objects instanciated of a particular class. Now, why is this pattern so complicated then? Because a software developer cannot use it 'freely', which means that the class candidate for applying a Singleton pattern, MUST satisfy a few conditions:  
- First of all, and the most obvious one is that you can't instantiate an object in two different parts of an application at the same time. Every single time you instantiate an object, you'll get the first object ever created. Keep that in mind. (Although there might be several implementations).    
- The Singleton class has Global Access, which means that it is in scope on any single line of code in your program.  
Several authors have their own opinion on the Singleton Pattern, some of then say that it's deprecated, others like it, and... You'll actually find tons of opinions out there. My personal opinion is:  
##### Try to avoid this pattern unless you're 100% sure of that individual instantiation. And even if you're 100% sure, take a look back, because 'Single' may have to turn into 'Multiple' in the future.  
#### How do you use it?  
Fair enough with all the philosophycal stuff, let's implement a Singleton with a Java example. You may have notice that when we are creating our classes in Java (or pretty much any other Object Oriented programming language), the constructor of that class will 'by default' be public. Many people don't actually think about this and just type it, but public constructor = anywhere instantiation. Here is when Singleton comes in hand. We'll make that class' constructor private, and then create a static method that will return the object itself, but hey, always checking if an instance has already been created.  
Time to go for an example: We are building an HTTP Server in Java and we want a class to handle the configuration files to load them at the beginning of our application. Notice that the class will only be instatiated once (on start) and we just want an instance running on our program, enough for using the Singleton Pattern. Our class will look like this:  
```
public class ConfigurationLoader{
  ConfigurationLoader instance = null;
  
  //Set constructor to private
  private ConfigurationLoader() {}
  
  public static getInstance(){
    if(this.instance == null) {
      this.instance = new ConfigurationLoader();
    }
    return this.instance;
  }
}
```  
Now that we have our Singleton class implemented, we can create only an instance of that class in our program. Each time we would like to create a new object, the first one will be returned.  
```
ConfigurationLoader firstLoader = ConfigurationLoader.getInstance(); //First object ever created  
ConfigurationLoader secondLoader = ConfigurationLoader.getInstance(); //secondLoader has the same instance as firstLoader
```  
And that's it! We've just implemented a singleton pattern.  
