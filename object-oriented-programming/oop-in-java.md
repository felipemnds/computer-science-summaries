[< MENU](https://github.com/felipemnds/computer-science-notebook/blob/master/README.md)

>  ***References List:***
> 1. https://classroom.udacity.com/courses/ud283

# Part 1. The World of Objects
First, let's understand very well what Object Oriented Programming really looks like.
## 1) What is OOP?
Video that explains what's Object Oriented Programming: [https://youtu.be/1Wjm_MJ_WfQ](https://youtu.be/1Wjm_MJ_WfQ)  

## 2) Fields
For example a *book* object may contain fields like *title*, *author* and *numberOfPages*. Then a library object may contain a field *named* books that will store all *book* objects in an array.
**Accessing a field** in an object is done using the dot modifier ‘.’  

    String title;
    String author;
    int numberOfPages;

To **access** the title field you would use:    

    book.title

## 3) Methods
To **use a method** you call it (just like calling a function). This is also done using the dot modifier.

## 4) Objects & Classes
-   **CLASS** - a guide that contains fields and methods
   
-   **OBJECT** - a variable created based on the class, with specific values

| | Class | Object |
|--|--|--|
| **What:** | A Data Type | A variable |
| **Where:** | Has its own file | Scattered around the project |
| **Why:** | Defines the structure | Used to implement to logic |
| **Naming convention:** | CamelCase | camelCase |
| **Examples:** | Country | australia |
|| Book | lordOfTheRings |
|| Pokemon | pikachu |

In summary, **objects** are to **Classes** what **variables** are to **Data types**.
**String** is a class! That's why it's written with uppercase letter.
**Everything in Java is an object:**

|Class| Primitive type |
|--|--|
| Integer | int |
| Long| long|
| Double| double |
| Character| char |
| String| char[] |

Each of those classes is made up of the corresponding primitive type as its field, but usually also comes with some powerful methods.

## 5) The _main_ method
This is the method that will start a program the very first time:

    public static void main(String [] args){
        // Start my program here
    }

Let's break it down:
-   **public**: Means you can run this method from anywhere in your Java program (we will talk more about public and private methods later
-   **static**: Means it doesn't need an object to run, which is why the computer starts with this method before even creating any objects (we will also talk more about static methods later on)
-   **void**: Means the main method doesn't return anything, it just runs when the program starts, and once it's done the program terminates
-   **main**: Is the name of the method
-   **String [] args** : Is the input parameter (array of strings) which we will cover how to use it later in this lesson as well!
 

## 6) Constructors

Constructors are special types of methods that are responsible for creating and initializing an object of that class.
**Creating a constructor** is very much like creating a method, except that:
1.  Constructors don't have any return types
2.  Constructors have the same name as the class itself

They can however take **input parameters** like a normal method, and you are allowed to create multiple constructors with different input parameters.

To create an object of a certain class, you will need to use the new keyword followed by the constructor you want to use, for example:  

    Game tetris = new Game();

To create a game that is initialized with a different starting score you can use the second constructor:  

    Game darts = new Game(501);

In some cases, you might want to explicitly set an object to null to indicate that such object is invalid or **yet to be set**. You can do so using the assignment operation:

    Game darts = null;

### Q: Why multiple constructors?
Good point, however, it's considered a good practice to always include a default constructor that initializes all the fields with values that correspond to typical scenarios.
### Q: But you said the default constructor is optional!
However, this privilege goes away once you create any constructor of your own! Which means if you create a parameterized constructor and want to also have a default constructor, you will **have to** create that default constructor yourself as well.

## 7) Self Reference
Sometimes you'll need to refer to an object within one of its methods or constructors, to do so you can use the keyword _this_.
For example, if a Position class was written like this

    class Position {
        int row = 0;
        int column = 0;
        //constructor
        Position(int r, int c) {
            row = r;
            column = c;
        }
    }

A more readable way would be to use the same names (row & column) for the constructor parameters which means you will have to use the this keyword to seperate between the fields and the paramters:

    class Position {
        int row = 0;
        int column = 0;
        //constructor
        Position(int row, int column) {
            this.row = row;
            this.column = column;
        }
    }

## 8) Public vs Private (for Fields and Methods)
### A) Fields  
To label a field as private or public simply add the modifier just before the field type when declaring it:

    public int score;
    private String password;

It's strongly recommended in Java to label ALL fields as private.  

For example , when defining a Book class, instead of saying:

    class Book{
        String title;
        String author;
    }
A proper way would be to define everything private, and only initialize them in the construtor.

    class Book{
        private String title;
        private String author;
        public Book(String title, String author){
            this.title = title;
            this.author = author;
        }
    }
This way you can guarantee that once a book object has been created, the title and author will never change!

**Better Design:** using _GETTERS_ and _SETTERS_
1.  GETTERS - Create a public method that returns each private field, so you can read the value without mistakingly changing it
2.  SETTERS - Create a public method that sets each private field, this way you will know when you are changing a field
### B) Methods
**Private methods** are usually known as **helper methods**, because they are there to organize and actually help **public methods**.
Here we have an example:
```
class Person{
   private String userName;
   private String SSN;
   private String getId(){
      return SSN + "-" + userName;
   }
   public String getUserName(){
      return userName;
   }
   public boolean isSamePerson(Person p){
      if(p.getId().equals(this.getId()){
         return true;
      }
      else{
         return false;
      } 
   }
}
```
The method `getId()` was set to private so that no other class can know the social security number of any person.

However, we were still able to use that method internally when comparing this person with another person object in the `isSamePerson(Person p)` method.

This means that any other class can only call `getUserName` or `isSamePerson` and will seem as if these are the only 2 methods provided by the class Person.
# :tada: 
# Part 2. Reading User Input
So now that we know how powerful OOP can be, let's learn how to make our code more interactive!
## 1) Input Scanner
You can ask the user to type in a message and the your Java program can read it into a variable and use it.

This is done using a Java class called `Scanner`.

But first, you have to point your program to the *java.util* library that includes the `Scanner` class.
```
import java.util.Scanner;
```
A `Scanner` allows the program to read any data type from a particular input, if we create the scanner object like this:
```
Scanner scanner = new Scanner(System.in);
```
Then the scanner will be reading from the System's input until the user hits "enter" then the program continues to execute.
Calling the method `nextLine()` in that scanner object will return a String that contains everything the user has typed in before they hit "enter".

```
scanner.nextLine();
```

### For example:
```
System.out.println("Enter your address: ");
Scanner scanner = new Scanner(System.in);
String address = scanner.nextLine();
System.out.println("You live at: " + address);
```
The above code will wait until the user types in their address, then stores it into the variable `address` and then prints it back to the user.

If you want to read a number into an integer variable instead of the entire line:

```
System.out.println("Enter your grade: ");
Scanner scanner = new Scanner(System.in);
int grade = scanner.nextInt();
if(grade > 90){
   System.out.println("Wow! you did well!");
}else{
   System.out.println("Not bad, but you can do better next time!");
}
```
## 2) File Scanner
To read a text file in Java you can also use the same `Scanner` class we used to read command line inputs, but instead of passing `System.in` as the argument you pass a `File` object which you can create by typing in the file name:
```
File file = new File("expenses.txt");
Scanner fileScanner = new Scanner(file);
```
Once the file scanner has been created, you read lines the same way we did earlier.
But since you would most likely want to load the entire file at once, you can check if the file still has more lines using `hasNextLine` method and then use this loop to read everything:
```
while (input.hasNextLine()) {
   String line = input.nextLine();
   // Use that line to do any calculations, processing, etc ..
}
```
And for this, you need another library as well:

    import java.io.File;
    
## 3) Exceptions
**Exceptions** are potential problemas like *invalid inputs* or *files that doesn't exist*.

> [Video that explains the dynamics of throwing, try & catch.](https://youtu.be/qTOk2-jf260)
> [Video that explains Exception Handling in a more complete way.](https://www.youtube.com/watch?v=W-N2ltgU-X4)

Exceptions will be *thrown* by your methods by simpling putting `throws Exception` right after your method's name. **You** have the responsability to catch it, giving the user a good and friendly experience with your program.
```
try{
   openFile("somefile.txt");
   array[index]++;
} catch(FileNotFoundException exception) {
   // Handle all the possible file-not-found-related issues here
} catch(IndexOutOfBoundsException exception) {
   // Handle all the possible index-out-of-bounds-related issues here
} 
```
Keywords that are importants for Exception Handling:
1. **try** - block that will throw the exception
2. **catch** - block that will handle the thrown exception
3. **finally** - block that will always be executed
4. **throw** - throws a single exception
5. **throws** - goes with a method
List of *Built In* exceptions:
- ArithmeticException
- ArrayIndexOutofBoundException
- ClassNotFoundException
- IOException
- InterruptedException
- NoSuchFieldException
- NoSuchMethodException
- NumerFormatException
- RuntimeException
- StringIndexOutofBoundException
# Part 3. There's more to OOP
Creating good aplications includes:
1. **Encapsulation** - each class contains everything it needs and nothing more
2. **Polymorphism** - multiples shapes of forms
3. **Inheritance** - passing down traits from a parent to their child
## 1) Inheritance 
1. Create a "A" class that contains common fields and methods. This one's called "parent";
2. Create other classes "B", "C", "D" (as much as you want) with the expression `extends A`. Those classes are called "chid".
## 2) Polymorphism
1. Create "Person" class with `name` and `email`;
2. Create "Student" and "Teacher" that `extends Person`;
3. You can declare them in multiple ways:
	- `Student student = new Student();`
	- `Person student = new Student();`
4. To make shure the actual object has a specific instace, just use the `instanceof`keyword:
```
if (contaBancaria instanceof Conta Poupance){
	// Code
}
```
## 3) Override methods
`Student`will have all methods inside `Person`, but it's child can **override** methods if needed, just by rewriting it.
1. If it's child just rewrites the method, it will be **overrided**, ignoring the original 
2. If you want to use the original method's code, include the `super.method()` to use the original method's code or `super()` to use it's constructor
## 4) Interface (multiple inheritance problem)
> [Video that shows how Interface works.](https://youtu.be/_2Kd4RUlWUg)

Creating an `interface` is very similar to creating a `class`. Interfaces define what a class show **do** but not **how** to do it:
```
// movable.java
public interface Movable{
	void move(int distance);
	boolean canMove();
}
// habitable.java
public interface Habitable{
	boolean canFit (int inhabitants);
}
```
With all the Interfaces done, a class can use them with the **implement** keyword:
```
// caravan.java
public class Caravan implements Habitable, Movable{
}
```
Note: this class **needs** to implement his *interfaces* methods.
## 5) Final Methods/Fields
But if you want to make sure no one will override your **method**? Simple!
Just remember to include the keyword `final` on your method declaration.
You cant use the keyword `final`with **fields** as well. This way, nothing will change this field's value after it's declared.
## 6) Static
### Static fields
* will belong to the *class*, not the objects (it's independent);
* will be shared throught all the class's objects;
* it can be changed normally;
* can be accessed directly without needing an object (`Class.field`);
### Static methods
* will belong to the *class*, not the objects (it's independent);
* can be accessed directly without needing an object (`Class.method`);
* takes input arguments and returns a result based only on those input values and nothing else;
* can still access static fields (because they also belong to the class);
## 7) Protected 
Any member that has the keyword `protected` can only be accessed by it's subclass (child).
## 8) Abstract
When used, a **class** can't be instaciated directly by it's parent, and obblies a child to implemente it's parent's **method**.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4ODkzNzI5NSwxNzU4ODE5MjIwLDEzMT
k5ODM1ODEsMTE3NTYyNzQ5MywxNTM4MTY5MDYxLDE5MTE4NTEy
MjgsMTQxOTE0MTY2LC0zNDU3NzQ4MCwtNTM4NzU5NzA1LC0yMT
QzNjc3MzcyLC0yOTM2MDAwOTYsLTE5MzkyNzIzMjksMTgxMzA2
MjM2MiwxODM2NzA3NTkxLDE2MDY2OTg0OTMsMzg0NjQ4MDMyLD
E5OTQzNDUyMDMsMTA5NDY2NjI0MCw5MDk1MjE0NjEsLTQ2ODY3
MjI3N119
-->