
# Singleton

## What ?
    - ensure class has only one instance
## Why ?
    - provide global access to that instance
## Usage ?
    - Logging class
    - Managing connection to DB
    - File manager
    - thread pools, configuration settings, device driver objects.
## How to create ?
    - declare all constructors of the class as private
    - provide a static method that returns a reference to the instance
## When not to use ?
    - You know how often you use globals? Ok, now use Singletons EVEN LESS. Much less in fact.
    - They share all the problems globals have with hidden coupling
## Example in java ?
    `java.lang.Runtime#getRuntime()`
## Code example 

```class Singleton
{

    private static Singleton single_instance = null;

    public String s;

    private Singleton()
    {
        s = "Hello I am a string part of Singleton class";
    }

    public static Singleton getInstance()
    {
        if (single_instance == null)
            single_instance = new Singleton();

        return single_instance;
    }
}
```