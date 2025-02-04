##### Annotations are used to provide supplemental information about a program. 
- Annotations start with ‘**@**’.
- Annotations do not change the action of a compiled program.
- Annotations help to associate _metadata_ (information) to the program elements i.e. instance variables, constructors, methods, classes, etc.
- Annotations are not pure comments as they can change the way a program is treated by the compiler. See below code for example.
- Annotations basically are used to provide additional information, so could be an alternative to XML and Java marker interfaces.
```
// Java Program to Demonstrate that Annotations
// are Not Barely Comments

// Class 1
class Base {

	// Method
	public void display()
	{
		System.out.println("Base display()");
	}
}

// Class 2
// Main class
class Derived extends Base {

	// Overriding method as already up in above class
	@Override public void display(int x)
	{
		// Print statement when this method is called
		System.out.println("Derived display(int )");
	}

	// Method 2
	// Main driver method
	public static void main(String args[])
	{
		// Creating object of this class inside main()
		Derived obj = new Derived();

		// Calling display() method inside main()
		obj.display();
	}
}

```
**OUTPUT**
```
10: error: method does not override or implement
    a method from a supertype
```