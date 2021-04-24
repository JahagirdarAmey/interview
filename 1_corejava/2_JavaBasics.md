**1. What is java? and its advantages**
- Object Oriented Programming Language
- PI / Portable 
- Multi threaded
- Secure (?)
- Rich in libraries / framework
- Provides exception handling 
- Robust because of garbage collection 

**2. Is java 100% object oriented ?**
- No, As it contains primitive types such as int, float, double.  


**3. What is JVM ?**
- Java virtual machine 
- Which can execute java bytecode 

**4. Why is Java called the Platform Independent Programming Language?**
- No need to re-write or re-compile 
- JVM takes care

**5. Is JVM Platform specific? Why ?**

**6. JDK vs JRE ?**
- JRE 
	- is where java programs are being executed 
	- It is a jvm implementation 
- JDK is SDK for Java including JRE + development tools (compilers, debugger)

**7. Static**
- Static variable
	- No need to instantiate java object. Can be called directly using java class
	- Accessing not-static variables in static context
		- A static variables belong to class & its value remains same for all its instances 
		- A static variable is initialized when the class is loaded by the JVM. 
		- If your code tries to access a non-static variable, without any instance, the compiler will complain, because those variables are not created yet and they are not associated with any instance.
- Static method
	- No need to instantiate java object. Can be called directly using java class
	- Static method can not be overridden. Why ? -  method overriding is based upon dynamic binding at runtime and static methods are statically bound at compile time.
- Static class
- Static block 	

**8. Primitive data types in java** 
- byte
- short
- int
- long
- float
- double
- boolean
- char

**9. What is Autoboxing and Unboxing?**
- Autoboxing is the automatic conversion made by the Java compiler between the primitive types and their corresponding object wrapper classes. - int to an Integer, a double to a Double, and so on. 
- If the conversion goes the other way, this operation is called unboxing.
- Wrapper classes 
	- java primitives into objects
	

**10. What is Function Overriding and Overloading in Java?**
- Overloading - two or more methods in the same class have the exact same name, but different parameters. 
- Overriding -  when a child class redefines the same method as a parent class. Overridden methods must have the same name, argument list, and return type. 

**11. Constructor** 
- A constructor gets invoked when a new object is created.
- Every class has a constructor. In case the programmer does not provide a constructor for a class, the Java compiler (Javac) creates a default constructor for that class.
- Constructor overloading - similar to method overloading
- Constructor in abstract classes (?)
- Constructor can not be called directly from method
- Copy-constructor 
	- Difference from C++ - Java does not create a default copy constructor if you do not write your own.
	```
    public class Employee extends Person{  
    		private String name;
     
    		public Employee(String name){
     		 this.name = name;
    		}
     
    		public Employee(Employee emp){
      		this.name = emp.name;
    		}
	} 
	```
 
**12.Does java support multiple inheritance ?**
- No, A class can extend one class only, But can implement multiple inheritance. 
- Diamond Problem - Refer Java 8 

**13. Interface** 
- All methods in interface are abstract implicitly (Explicit abstract is NOT allowed?)
- Variables are final implicitly. (Explicit final is allowed) 
- Members & methods are public by default. (Can it be private ? - NO)
- Implementing class must implement abstract methods
- Cannot be instantiated

**14. Abstract** 
- Abstract class may contain abstract methods and non-abstract(concrete) methods 
- Implementing class must implement abstract methods, If does not, Implementing class also must be abstract 
- Abstract classes can implement interfaces without even providing the implementation of interface methods.
- An abstract class may contain non-final variables.
- An abstract class also cannot be instantiated but can be invoked if it contains the main method.
- Abstratc class may not contain abstract methods 

**15. What are pass by reference and pass by value?**
- Pass by value 
	- When an object is passed by value, this means that a copy of the object is passed.
```java
public class ComputingEngine
{
	public static void main(String[] args)
	{
		int x = 15;
		ComputingEngine engine = new ComputingEngine();
		engine.modify(x);
		System.out.println("The value of x after passing by value "+x);
	}
	public  void modify(int x)
	{
		x = 12;
	}
}
```
- Pass by reference
	- When an object is passed by reference, this means that the actual object is not passed, rather a reference of the object is passed.
	- Thus, any changes made by the external method, are also reflected in all places.
```java
	public class ComputingEngine 
	{ 
	    public static void main(String[] args) 
    	    { 
         
        	ComputingEngine engine = new ComputingEngine();
         
		
		Computation computation = new Computation(65);
        	engine.changeComputedValue(computation);
         
        	System.out.println("The value of x after passing by reference "+ computation.x);
	    } 
     
   	 public void changeComputedValue(Computation computation)
    	   {
        	computation = new Computation();
        	computation.x = 40;
    	   }
	}
  
	class Computation 
	{ 
    		int x; 
    		Computation(int i) { x = i; } 
		Computation()      { x = 1; } 
	}


```

16. Local variables vs instance variables 
- Local variabls 
	- inside method or constructor or block
	- Need to be initialised, Oterwise code will not compile.
- Instance varaibes
	- Inside class or class level
	- If not initialised, default value is used

17. Access modifiers 
- Public - accessible from everywhere in app
- Protected - accessible within the package and the subclasses in any package
- Package Private (Default) – accessible strictly within the package
- Private – accessible only within the same class where it is declared

**18. Difference between static binding and dynamic binding**
- Static binding 
	- Binding at compile time 
	- Shape s = new Shape();
- Dynamic binding 
	- Binding at run time
	- Shape s = new Rectangle();

19. What’s the difference between String, StringBuffer andStringBuilder?

**String pool**
**String with new & without new**
**String immutability**

**Shallow copy, Deep copy & Cloneable**
- 
```
// Shallow Copy 
public class ShallowCopy {

    int i;

    public static void main(String[] args) {

        ShallowCopy shallowCopy = new ShallowCopy();
        shallowCopy.i = 10;

        System.out.println(" Initial " + shallowCopy.i); // 10

        ShallowCopy shallowCopy1 = shallowCopy;
        shallowCopy1.i = 5;

        System.out.println(" After " + shallowCopy.i); // 5
    }
}


// Deep copy - Creates new object 
obj2.i = obj.i;

// Clonable 
Obj2 = Obj.clone()
```

**Object Cloning**

**Method overloading by changing the return type**
**Override private methods**

**Constructor Chaining**

**This keyword**
**Super Keyword**

**equals vs ==**

**Explain toString() method**
- The toString() method returns the string representation of the object.
```
class Student{  
 int rollno;  
  
 Student(int rollno){  
    this.rollno=rollno;  
 }  

 public String toString(){//overriding the toString() method  
  return rollno;  
 }  
  
 public static void main(String args[]){  
   Student s1=new Student(101);  
   
   system.out.println(s1);

//1. If toString is NOT overloaded - Student@1fee6fc  
//2. If toString is overloaded - 101
     
 }  
}  
```


**Explain marker interfaces**
- A marker interface is an interface that has no methods or constants inside it. 
- It provides run-time type information about objects, so the compiler and JVM have additional information about the object.

**instanceOf operator**
**Atomic operation in Java**

**JIT Compiler**
- Performance improvement 
- Reduces amount of time needed for compilation 

**Explain public static void main(String args[ ]) in Java**
- public: Public accessibility of the method. Any Class can access the main() method.
- static: The keyword indicates the method is a class method. The method main() is made static so that it can be accessed without creating the instance of the class. When the method main() is not made static, the compiler throws an error because the main() is called by the JVM before any objects are made, and only static methods can be directly invoked via the class.
- void: Return type of the method - void - does not return any type of value.
- main: JVM searches this method when starting the execution of any program, with the particular signature only.
- String args[]: The parameter passed to the main method.

**Can we overload main() method?**
- main method can be overloaded in a similar manner, JVM always looks for the method signature to launch the program.
- The normal main method acts as an entry point for the JVM to start the execution of program.
- We can overload the main method in Java. But the program doesn’t execute the overloaded main method when we run your program, we need to call the overloaded main method from the actual main method only.

**How to make class immutable**
- Declare class as final so it can not be overloaded 
- Make all fields private so direct access is not allowed 
- Do not provide setter methods 
- Initialize all the fields via a constructor performing deep copy
- Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.

**What is reflection in java?**
- Reflection is used to load java classes at runtime. 
- Frameworks like struts, spring and hibernate uses reflection for loading classes at runtime.

**Inner classes vs sub classes**
Inner Class 
- Class within another class, Nested class
- An inner class has access rights for the class which is nesting it. Means it can access varaibles and methods of outerclass  
Subclass
- Child class of another class 
- Can access public and protected methods 


**Instance variable vs local veriable**
Instance variable - Class level variable
Local variable - method level variable 

**Char array vs String for storing sensetive information**
Char array is preffered as String is immutable and any modification in string produces new string, String values will be kept in spring pool (heap) until GC happens, So If someone got memory dump access, It can cause security isssues

**Continue or Break**
Continue 
- Currant iteration is broken 
Break
- Loop is broken 

**Default in switch**
- Optional 
- Always written at last


**Main method in java**
- Can not return anything deu to signature resiction 
- Can not be private as JVM will not be able to invoke it. Runtime error

**Interface vs abstract performance implecations**
- Interfaces are slow than abstact 
- interface needs extra indiracions 
- Only 1 class can be extended but many interfaces can implement causes an compulson to implement each and every interface method 

**Importing Package can also import sub-pacges ?**
No

