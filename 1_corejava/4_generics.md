**1. What is Generics in Java ? What are advantages of using Generics?**
- Those who are coming from prior to Java 5 background knows that how inconvenient it was to store object in Collection and then cast it back to correct Type before using it. Generics prevents from those. 
- It provides compile time type-safety and ensures that you only insert correct Type in collection and avoids ClassCastException in runtime.

**2. How Generics works in Java ? What is type erasure ?**
- Generics is implemented using Type erasure, compiler erases all type related information during compile time and no type related information is available during runtime. 
  for example List<String> is represented by only List at runtime.
- This was done to ensure binary compatibility with the libraries which were developed prior to Java 5. 
  you don't have access to Type argument at runtime and Generic type is translated to Raw type by compiler during runtime. 

**3. What is Bounded and Unbounded wildcards in Generics ?**
- Bounded Wildcards are those which impose bound on Type. there are two kinds of Bounded wildcards <? extends T>  which impose an upper bound by ensuring that type must be sub class of T and <? super T> where its imposing lower bound by ensuring Type must be super class of T. 
- This Generic Type must be instantiated with Type within bound otherwise it will result in compilation error. On the other hand <?> represent and unbounded type because <?> can be replace with any Type. 

**4.What is difference between List<? extends T>  and  List <? super T> ?**
- Both of List declaration is example of bounded wildcards, 
- List<? extends T> will accept any List with Type extending T while List<? super T> will accept any List with type super class of T. 

**5. How to write a generic method which accepts generic argument and return Generic Type?**
```java
public V put(K key, V value) {
return cache.put(key, value);
}
```

**6. Generics clas ?**
Consider the class below:

```java
class MyList {
private List<String> values;

    void add(String value) {
        values.add(value);
    }

    void remove(String value) {
        values.remove(value);
    }
}
```
MyList can be used to store a list of Strings only.

```java
MyList myList = new MyList();
myList.add("Value 1");
myList.add("Value 2");

```
To store integers, we need to create a new class. This is problem that Generics solve. 
Instead of hard-coding String class as the only type the class can work with, we make the class type a parameter to the class.

Example with Generics
Let’s replace String with T and create a new class. Now the MyListGeneric class can be used to create a list of Integers or a list of Strings

```java
class MyListGeneric<T> {
private List<T> values;

    void add(T value) {
        values.add(value);
    }

    void remove(T value) {
        values.remove(value);
    }

    T get(int index) {
        return values.get(index);
    }
}
```

```java
MyListGeneric<String> myListString = new MyListGeneric<String>();
myListString.add("Value 1");
myListString.add("Value 2");

MyListGeneric<Integer> myListInteger = new MyListGeneric<Integer>();
myListInteger.add(1);
myListInteger.add(2);

****
```

**7. Can we use Generics with Array?**
- Array doesn't support Generics and that's why Joshua Bloch suggested in Effective Java to prefer List over Array because List can provide compile time type-safety over Array.

**8. Difference between List<Object> and raw type List in Java?**
- Main difference between raw type and parametrized type List<Object> is that, compiler will not check type-safety of raw type at compile time but it will do that for parametrized type and by using Object as Type it inform compiler that it can hold any Type of Object e.g. String or Integer.
- you can pass any parametrized type to raw type List but you can not pass List<String> to any method which accept List<Object> it will result in compilation error.

**9. Difference between List<?> and List<Object> in Java?**
- List<?> is List of unknown type while List<Object> is essentially List of any Type. 
- You can assign List<String>, List<Integer> to List<?> but you can not assign List<String> to List<Object>.

**10. Difference between List<String> and raw type List.**
```java
List listOfRawTypes = new ArrayList();
listOfRawTypes.add("abc");
listOfRawTypes.add(123); //compiler will allow this - exception at runtime
String item = (String) listOfRawTypes.get(0); //explicit cast is required
item = (String) listOfRawTypes.get(1); //ClassCastException because Integer can not be cast in String
     
List<String> listOfString = new ArrayList();
listOfString.add("abcd");
listOfString.add(1234); //compiler error, better than runtime Exception
item = listOfString.get(0); //no explicit casting is required - compiler auto cast
```