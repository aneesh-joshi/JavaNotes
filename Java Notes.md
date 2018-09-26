Java Notes
- Static initializers are blocks of executable code hat may be used to help initialize a class when it is first loaded.
- Static import feature allows to access classes of a package without package qualification 
- Static declaration inside a method change the lifetime of a variable
- Static Methods: A method that is declared static is called a class method. A class method is always invoked without reference to a particular object.
- final: can be assigned once or zero time
- transient: not stored or saved via the standard serialization process
- volatile: A variable may be modified by multiple threads. This gives a hint to the compiler to fetch the value each time, rather store a locale copy. This also prohibits same optimization procedures.
- http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-100.html
- arrays are passed by reference
- http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-103.html
- http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-104.html : We can make circular execution by declaring a constructor as an instance variable. This will compile but will get stuck in an infinite loop while running.
- Some declarations may be shadowed in part of their scope by another declaration of the same name, in which case a simple name cannot be used to refer to the declared entity. https://docs.oracle.com/javase/specs/jls/se7/html/jls-6.html#jls-6.4.1
- Can have multiple initialization scopes with switch case if it is bracketed. http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-106.html
- Can static variables be declared inside of a method? --> No, not even in static methods
- All doubts : http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-107.html
- Autoboxing is the automatic conversion that the Java compiler makes between the primitive types and their corresponding object wrapper classes. For example, converting an int to an Integer, a double to a Double, and so on. If the conversion goes the other way, this is called unboxing.
- The members of a class type are all of the following:
	• Members inherited from its direct superclass, except in class Object, which has no direct superclass
	• Members inherited from any direct super interfaces
	• Members declared in the body of the class.
	• Is a relationship
private memebers are not inherited.  Only members of a class that are declared protected or public are inherited by subclasses declared in a package other than the one in which the class is declared.
Constructors and static initializers are not members and therefore are not inherited.
- getClass() -> toStr -> return class className

- When you type cast a child to its parent: 
	- variables access specific variables of each class. 
	- functions always refer to the child's functions
Example:

class Parent{
    int x;

    Parent(){
        x = 69;
    }

    Parent(int x){
        this.x = x;
    }

    void sayHello(){
        System.out.println("Hello from parent!");
    }
}

class Child extends Parent{
    int x;
    Child(){

    }

    void sayHello(){
        System.out.println("Hello from child!");
    }

    Child(int x){
        this.x = x;
    }

    public static void main(String[] args) {
        Child child = new Child(42);

        System.out.println("child.x " + child.x);
        System.out.print("child.sayHello() "); child.sayHello();
        System.out.println();

        Parent parent = child;
        System.out.println("parent.x " + parent.x);
        System.out.println("((Parent)child).x " + ((Parent)child).x);
        System.out.print("((Parent)child).sayHello() "); ((Parent)child).sayHello();
        System.out.println();
    }

}

Output:
child.x 42
child.sayHello() Hello from child!

parent.x 69
((Parent)child).x 69
((Parent)child).sayHello() Hello from child!


- A member type or a constructor of a class type is accessible only if the type is accessible and the member or constructor is declared to permit access:
• If the member or constructor is declared public, then access is permitted.
• Protected methods and variables are accessible to subclasses and provide a way of opening up the encapsulation.
• Private methods and variables are not accessible to subclasses.
• A final class can not be sub classed.

- A package is a set of related classes. Classes in the same package can access each other's protected members.
- Inner classes cannot be declared as native, synchronized, transient or volatile. They can be static.
- You can even declare an inner class within a function
- About inner classes : http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-116.html
- VIMP question on casting http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-117.html

- An abstract class
	• specifies a public method interface which can be inherited by direct or indirect subclasses.
	• may declare methods, but not implement them.
	• can not be instantiated.
- Can also define non abstract functions within an abstract class
- Classes who extend an abstract class share the same, possibly extended, interface.
	• Is a relationship
- Still correct implementation of abstract

		abstract class AbstractParent{
		    int x;
		    
		    abstract void sayName(int lel);
		}

		class Child extends AbstractParent{
		    void sayName(int lrl){
		        System.out.println("Whazzup");
		    }
		}

- You can store child objects in a parent array even if parent isn't abstract
- If you do 

		String func1(){
			sout("World");
			return "!!!";
		}

		sout("Hello " + func1());

It'll print:

		World Hello !!!

i.e., the function prints are executed first. Be careful.

- Good question: http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-122.html

- This in parent still refers to the child object somehow (DOUBT)

		class Parent{
		    Parent(){
		        System.out.println("Parent " + this);
		    }
		}

		class Child extends Parent{
		    Child(){
		        System.out.println("Child " + this);
		    }
		}

		class Test{
		    public static void main(String[] args) {
		        Child child = new Child();
		    }
		}

Output:
		
		Parent Child@28864e92
		Child Child@28864e92


- Abstract qn: http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-124.html
- whenever you are casting stuff, always put brackets around it.
(A)aArray[i].isAbstract() -> wrong
((A)aArray[i]).isAbstract() -> correct

- Interfaces
	• An interface specifies which methods must be implemented.
	• An interface defines an public API.
	• This means, we can make sure, that unrelated classes share the same part of the interface.
	• An interface defines constants. They are public, static and final regardless of whether these modifiers have been specified.
	• Methods implementations have been added to be able to extend the funtionality by modifying the interface and not the implementations.
	• Interface methods can’t be native, static, synchronized, final, private, or protected
	• Abstract and native methods can’t have a body.
	• Fields in a field a static and final.

- Native keyword : The native keyword is applied to a method to indicates that the method is implemented in native code using JNI (Java Native Interface). native is a modifier applicable only for methods and we can’t apply it anywhere else. The methods which are implemented in C, C++ are called as native methods or foreign methods. https://www.geeksforgeeks.org/native-keyword-java/

- Interfaces can extend other interfaces (multiple interfaces) / An interface can extend or inherit from more than one interface, and can provide implementations: http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-125.html

- about `default` keyword : https://www.geeksforgeeks.org/default-methods-java/

- Good question on defult constructors: http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-128.html
The all constructors always call the default constructor unless super tells them otherwise.
Child(), Child(int x), Child(int x, int y) all call  Parent()

If you only want Child(int x) and Parent(int x), you'll have to make the Child constructor as:

		Child(int x){
			super(x);
			// do child things
		}

- about overloading:
	• Overloading of constructors is identical in behavior to overloading of methods. The overloading is resolved at compile time by each class instance creation expression.
	• If a class contains no constructor declarations, then a default constructor that takes no parameters is automatically provided:
	• If the class being declared is the primordial class Object, then the default constructor has an empty body.
	• Otherwise, the default constructor takes no parameters and simply invokes the superclass constructor with no arguments.
	• A compile-time error occurs if a default constructor is provided by the compiler but the superclass does not have a constructor that takes no arguments.

- This causes problems with the default constructor:

		class Parent{
		    Parent(int x){

		    }
		}

		class Child extends Parent{
		    

		    Child(int x){
		        System.out.println("In child constr");
		    }
		    public static void main(String[] args) {
		        new Child(3);
		    }
		}

- Using reflection API to get all functions of a class

		import java.lang.reflect.Method;

		class PrintClassName {

		    public static void printClassName(Object o)	{
		        System.out.println("o.getClass().getName() = " +
		                o.getClass().getName());
		    }

		    public static void printMethods(Object o)	{
		        Method[] m = o.getClass().getMethods();
		        for (int i = 0; i < m.length; i ++ )
		            System.out.println("m[" + i + "]\t=\t" +
		                    m[i].getName());

		    }

		    public static void main(String args[])	{
		        String aString = "aaa";
		        Integer aInteger = new Integer("0");

		        printClassName((Object)aString);
		        printClassName((Object)aInteger);

		        printMethods((Object)aInteger);
		    }
		}

- Nested classes:	
	• Nested classes can be: non-static or static nested.
	• Non-static nested classes are refered to as inner classes.
	• A nested class is a class that is a member of another class.

	class Outer{
	   . . .
	  class AnestedClass {
	          . . .
	  }
	}
	• A nested class can be declared static or not.
	• A static nested class is called a static nested class.
	• A non static nested class is called an inner class.
	• As with static methods and variables, a static nested class is associated with its enclosing class.
	• And like class methods, a static nested class cannot refer directly to instance variables or methods dfined in its enclosing class-it can use them only through an object reference.
	• As with instance methods and variables, an inner class is associated with an instance of its enclosing cass and has direct access to that object’s instance variables and methods.
	• Because an inner class is associated with an instance, it cannot define any static members itself.

- Inner classes are of 2 types:
	- static inner classes:
		can call them directly.
		can access their static members directly
		cannot access their instance variables without creating theor instance
	- instance/ nested inner classes
		- cannot call them from psvm (i.e., a static context)
		- have to call them from a method in outer class which is not static

		class Outer{
		    static class StaticInner{
		        int a = 34;
		        static int staticInt = 45;
		    }

		    class InstanceInner{
		        int a = 42;
		    }

		    void callInnerClass(){
		        System.out.println(new InstanceInner().a);
		    }

		    public static void main(String[] args) {
		        System.out.println(StaticInner.a); // cannot access non-static a from
		        // static class StaticInner
		        System.out.println(new StaticInner().a);
		        System.out.println(StaticInner.staticInt);
		        System.out.println(InstanceInner.a);
		        System.out.println(new InstanceInner().a); // Outer.this cannot be 
		        // referenced from a static context
		        System.out.println(new InstanceInner());// Outer.this cannot be 
		        // referenced from a static context
		        
		        System.out.println(new Outer.InstanceInner());// Outer.this cannot be 
		        // referenced from a static context
		        new Outer().callInnerClass();
		    }
		}

Another example



		class NestedClassEx {

		    public int inNestedClass;

		    void inNestedClass() {
		        System.out.println("NestedClass!inNestedClass");
		        (new AinnerClass()).aInnerClassM2();
		    }

		    static class AstaticClass {
		        static void aStaticClassM1() {
		            System.out.println("AstaticClass!aStaticClassM1");
		        }

		        void aStaticClassM2() {
		            System.out.println("AstaticClass!aStaticClassM2");
		        }
		    }

		    class AinnerClass {
		/*
		       	static void aInnerClassM1()	{
				System.out.println("AinnerClass!aInnerClassM1");
			}
		   NestedClassEx.java:15: inner classes cannot have static declarations
		        static void aInnerClassM1()     {
		 */

		        void aInnerClassM2() {
		            System.out.println("AinnerClass!aInnerClassM2");
		        }
		    }

		    public static void main(String args[]) {

		        AstaticClass.aStaticClassM1();


		        (new AstaticClass()).aStaticClassM2();

		        (new NestedClassEx()).inNestedClass();
		//         (new AinnerClass()).aInnerClassM2();
		    }
		}

- Static Initializer Blocks
	• Static initializer blocks are primarily used for initialization.
	• The code in a static initializer block is executed when the class is initialized/
	• A class can have more than one static initializer block.
- Useful thing about static blocks http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-136.html

- A parent can refer to a child, but a child cannot refer to a parent.
		
		Parent parent = new Child(); // correct
		Child child = new Parent(); //wrong

- Good example of how parent casting of child blinds the object but keeps the data stored.

		class Parent{
		    int x = 3;
		    void foo(){
		        System.out.println("Prent foo");
		    }
		}

		class Child extends Parent{
		    int x = 4;

		    void foo(){
		        x = 69;
		    }

		    public static void main(String[] args) {
		        Parent parent = new Child();
		        parent.foo();
		        System.out.println(parent.x);
		        System.out.println(((Child)parent).x);
		//        Child child = (Child) new Parent();
		//        child.foo();
		    }
		}

TODO:
- Understand Regex in Java
- Learn acess specifier table
- http://spiegel.cs.rit.edu/~hpb/Lectures/2181/605/605-111.html
- What is polymorphism, encapsulation?
- do all DOUBTS

Tips:
- when inspecting a program, see static members first, then the main method
- class variables are created before the first line of the constructor is initialized
- if sout(this) is there, check for a toString on that class
