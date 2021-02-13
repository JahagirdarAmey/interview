**1. What is OOPS ?**
- Language in which objects are first class citizens 
- Uses real world analogy like- inheritance, polymorphism, abstraction etc
- Manipulating these objects to get results is the goal of Object Oriented Programming.

**2. OOP Concepts ?**
- Inheritance
	- Inheriting the properties of parents 
- Abstraction 
	- Abstraction hide details
	- It separates implementation from class 
	- Real world example - How car engine works is hidden from driver, Need not know.
	- interface Car with getEngine method, VW | Maruti implements Car 
- Encapsulation 
	- Data hiding
	- principle of wrapping data (variables) and code together as a single unit.
	- It keeps data safe. 
	- Example - private salary, Exposing its value using getter
- Polymorphism 
	- polymorphism means many forms.
	- Real world example - A person can be child, husband, father
	- Java 
		- Compile time polymorphism
			- Static polymorphism 	
			- Method overloading 
		- Run time polymorphism 
			- Dynamic polymorphism
			- A function call to the overridden method is resolved at Runtime. 
			
			```
			Parent a; 
  
        	a = new subclass1(); 
        	a.Print(); 
  
        	a = new subclass2(); 
       		a.Print(); 
            ```

**3. Abstraction vs. Encapsulation ?**
- Encapsulation 
	- is more about "How" to achieve a functionality
	- Solves problem at implementation level
- Abstraction 
	- is more about "What" a class can do.
	- Solves problem at design level

**4.Association, Aggregations, Compositions**

Association
- Both Composition and Aggregation are the form of association between two objects
- Association is relation between two separate classes which establishes through their Objects. 
- Association can be one-to-one, one-to-many, many-to-one, many-to-many.
- Association - > Aggregation - > Composition


Composition : 
- when one class owns other class and other class can not meaningfully exist, when it's owner destroyed
- Human class is a composition of several body parts
- Since Engine is-part-of Car, the relationship between them is Composition. 

```
public class Body {
    private final Hand hand;  
       
    public Body(){
       hand  = new Hand();
    }
}

class Hand {
    private String whichHand;
}
```

Aggregation 
- While in the case of Aggregation, including object can exists without being part of the main object
- An Employee which is part of an Org, can exist without an Org and can become part of other org as well.
- Since Organization has Person as employees, the relationship between them is Aggregation. 
- Here is how they look like in terms of Java classes

```
public class Organization {
    private List employees;
}

public class Person {
    private String name;   
}
```

**5. UML Notations of Association, Aggregations, Compositions**
Associations ------------->
Aggragation  ------------<>
Composition  ------------<> // Diamond is filled

**6. Why do you think OOPS brought evolution?** 

**7. Cohesion**
High cohesion - loose coupling  