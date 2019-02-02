
* [Object-Oriented Programming Concepts](http://java.sun.com/docs/books/tutorial/java/concepts/index.html)
* [Access Modifiers](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_access_modifiers.htm)


* The `global` access modifier, which is more permissive than the `public` modifier and allows access across namespaces and applications.

## List
You can add elements to a list when creating the list, or after creating the list by calling the add() method. 
* lists don’t require you to determine ahead of time how many elements you need to allocate.
* You can add elements to a list when creating the list, or after creating the list by calling the add() method.
* List elements can be read by specifying an index between square brackets
* you can use the get() method to read a list element.
* Create a list and add elements to it:
```apex
List<String> colors = new List<String> {'red', 'blue'};

//Add elements to list after it has been created
List<String>  moreColors = new List<String>();
moreColors.add('orange');

```
* List syntax: `List<Data Type> variable name = new List<Data Type>();`

* List elements can be read by specifying an index between square brackets, just like with array elements. Also, you can use the get() method to read a list element.

```apex
// Get elements from a list
String color1 = moreColors.get(0);
String color2 = moreColors[0];
System.assertEquals(color1, color2);

//iterate over a list to read elements
for(Integer i=0; i<colors.size(); i++) {
    //write value to the debug log
    System.debug(colors[i]);
}
```

## Apex Class Definition

* Class methods can be called by triggers and other classes.
* public method
* private helper method - 
* built-in Messaging methods
* Apex class library
* class encapsulates the methods that are related to managing email
* member variables (attributes) 
* accessor methods to access attributes
* class member variables
* Instance methods access class member variables.
* Static methods are easier to call than instance methods because they don’t need to be called on an instance of the class but are called directly on the class name.

### sObject
* Every record in Salesforce is natively represented as an sObject in Apex. 
* The Account sObject is an abstraction of the account record and holds the account field information in memory as an object.
* Each Salesforce record is represented as an sObject before it is inserted into Salesforce.
* when persisted records are retrieved from Salesforce, they’re stored in an sObject variable.
* to create an sObject, you need to declare a variable and assign it to an sObject instance. The data type of the variable is the sObject type.
* For custom relationship fields, the API name ends with the __r suffix. 
* [Object Reference for Salesforce and Lightning Platform](https://developer.salesforce.com/docs/atlas.en-us.216.0.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)

All objects have a state and a behavior, things that objects know about itself and things that an object can do.
Variables are used to specify the state of an object, such as the object's Name or Type.  

A class can contain other classes, exception types, and initialization code.

An interface is like a class in which none of the methods have been implemented—the method signatures are there, but the body of each method is empty. To use an interface, another class must implement it by providing a body for all of the methods contained in the interface.

Methods are used to control behavior, such as getOtherQuotes or copyLineItems.

To define a class, specify the following:
* Access modifiers:
    * Must use one of the access modifiers (such as `public` or `global`) in the declaration of the top-level class.
    * You do not have to use an access modifier in the declaration of an inner level class.
* Optional definition modifiers (`virtual`, `abstract`, etc.)
* Required: The keyword `class` followed by the name of the class.
* Optional extensions and/or implementations

Syntax to define a class:
```apex
private | public | global 
[virtual | abstract | with sharing | without sharing]
class ClassName [implements InterfaceNameList] [extends ClassName]
{
    //the body of the class
}
```
* The `virtual` definition modifier declares that this class allows extension and overrides. You cannot override a method with the `override` keyword unless the class has been defined as `virtual`.
* The `abstract` definition modifier declares that this class contains abstract methods, that is, methods that only have their signature declared and no body defined.

### Apex Class Definition
```apex
private | public | global 
[virtual | abstract | with sharing | without sharing] 
class ClassName [implements InterfaceNameList] [extends ClassName] 
{ 
// The body of the class
}
```

### Class Variables
```apex
[public | private | protected | global] [final] [static] data_type variable_name 
[= value] 
```
### Class Methods
```apex 
[public | private | protected | global] [override] [static] data_type method_name 
(input parameters) 
{
// The body of the method
}
```
* Methods with a void return type are typically invoked as a stand-alone statement in Apex code. 
* void - the method does not return a value.
* In Apex, all primitive data type arguments, such as Integer or String, are passed into methods by value. 
* This fact means that any changes to the arguments exist only within the scope of the method.
* When the method returns, the changes to the arguments are lost.
* Non-primitive data type arguments, such as sObjects, are passed into methods by reference. 
* when the method returns, the passed-in argument still references the same object as before the method call.
#### Example: Passing Primitive Data Type Arguments
* This example shows how a primitive argument of type String is passed by value into another method.
* The debugStatusMessage method in this example creates a String variable, msg, and assigns it a value. 
* It then passes this variable as an argument to another method, which modifies the value of this String. 
* since String is a primitive type, it is passed by value, and when the method returns, the value of the original variable, msg, is unchanged. 
* An assert statement verifies that the value of msg is still the old value.
```apex
public class PassPrimitiveTypeExample {
    public static void debugStatusMessage() {
        String msg = 'Original value';
        processString(msg);
        // The value of the msg variable didn't
        // change; it is still the old value.
        System.assertEquals(msg, 'Original value');
    }

    public static void processString(String s) {
        s = 'modified value';
    }
}
```
#### Invoking a public method
```apex
EmailManager em = new EmailManager();
em.sendMail('Your email address', 'Trailhead Tutorial', '123 body');
```
### Static Methods and Variables
* You can use static methods and variables only with outer classes.
* Inner classes have no static methods or variables.
* Before an object of a class is created, all static member variables in a class are initialized, and all static initialization code blocks are executed.
* These items are handled in the order in which they appear in the class.
* A static method is used as a utility method, and it never depends on the value of an instance member variable. 
* Because a static method is only associated with a class, it can’t access the instance member variable values of its class.
* A static variable is static only within the scope of the Apex transaction.
* It’s not static across the server or the entire organization.
* The value of a static variable persists within the context of a single transaction and is reset across transaction boundaries. 
* For example, if an Apex DML request causes a trigger to fire multiple times, the static variables persist across these trigger invocations.
* All instances of the same class share a single copy of the static variable.
* recursive trigger - trigger that calls itself.
* define the static variables in a class so that the trigger can access these class member variables and check their static values.
* A class static variable can’t be accessed through an instance of that class.
* Local variable names are evaluated before class names.
* Instance methods and member variables are used by an instance of a class, that is, by an object.
* Instance of a class === object
* An instance member variable is declared inside a class, but not within a method.
* Instance methods usually use instance member variables to affect the behavior of the method.
#### Using Initialization Code
* The instance initialization code in a class is executed each time an object is instantiated from that class. 
* These code blocks run before the constructor.

### Inheritance
* OOP suggests that you do not modify the existing code but extend it so that testing can be done only on the new code and there are fewer maintenance issues. === inheritance
* To use inheritance in Apex, we need to use the `virtual` or `abstract` keywords in the base class and methods.
* `virtual` keyword states that a class or method can be inherited and overridden by child classes. 
* `extends` keyword is used in a child class to inform a parent class.
* If we are writing the same method again in a child class of a parent class, then the `override` keyword needs to be used. 
* `override` keyword informs Apex that this is a new version of the same method in the parent class. 
* If we want to call any method in a parent class, we need to use the `super` keyword.
* a child class is able to reuse a parent class method with an added behavior. 
* The type of object is Mario, which is the parent class, but Apex is able to call a method of the Mario_Runclass using dynamic dispatch, which is a kind of Polymorphism.
* Assigning a child class reference to a parent class is known as subtype polymorphism.
#### Static and dynamic dispatch
* Types of polymorphism can be identified on the basis of when an implementation is selected. 
* when an implementation is selected at compile time, it is known as static dispatch. 
* When an implementation is selected while a program is running (in case of a virtual method), it is known as dynamic dispatch.
#### Interface
* `interface` is another way to achieve polymorphism and abstraction in Apex. 
* We cannot instantiate interfaces
* we can assign any child class to them
* Huge applications and APIs are created using interfaces. 
* `Queueable` and `Schedulable` are examples of interfaces.
*  Apex only needs to invoke the `execute()` method in your class because it knows that you follow the contract of an `interface`.
* Apex does not support multiple inheritance where one child class extends multiple parent classes at a time. However, using an `interface` a child class can implement multiple interfaces at a time.
### Abstract Classes
* In inheritance, a child class extends a parent class, where both the classes have full implementations. 
* In an interface, a parent class does not have any implementation and depends on child classes completely. 

```apex
public abstract class GameCoin { 
     
  public abstract Integer coinValue(); 
     
  public Integer absorbCoin(Integer existingPoint){ 
    return existingPoint + coinValue(); 
  }  
} 
```

* we cannot instantiate an abstract class
### Advantages of Design Patterns
* Coupling measures the dependency of software components on each other.
    * this is how two components interact with each other and pass information.
* robustness of the code:  the impact it has on a component if any related component is modified.
* low coupling indicates a good code structure.
* Cohesion measures the degree to which a code component has been well built and focused.
* Encapsulation - all the related data and functionalities should be encapsulated in the same program component (for example, a class). 
    * It ensures that all related functionalities are present in one place and controls their accessibility. 
    * Lower code cohesion indicates lower dependency of modules/classes, that is, higher maintainability, less complexity, and lesser impact on the part of change.
* high cohesion is better for you and indicates that a class is doing a well-defined job. 
* Low cohesion means that a class is doing many jobs with little in common between jobs.
* In Apex, a static variable lasts for the duration of an individual user request execution only (until the time the user request is being processed on a server). 
### The single responsibility principle (SRP)
The advantages of SRP are as follows:
* It makes code as easy as possible to reuse
* Small classes can be changed easily
* Small classes are more readable