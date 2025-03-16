# Fuctional Programming in Java

### Features of java 
- **Imperative Language**
Any piece of code is written as series of steps.
- **Object Oriented Language**
pretty much everything in java is object oriented.
- **Functional Language**
It has fuctional capabilities even though it is not purely fucntional.

### Functional Programming 
Functional programming is a programming paradigm where programs are constructed by applying and composing functions.

### Object Oriented Programming 
Object Oriented programming is a programming paradigm where programs are constructed by creating, applying and composing Objects, Types and classes.

### What is an function?

- **Sequence of instructions**
- **Possibly imperative within itself**
- **Forms a reusable unit**

A function or subroutine is a sequence of program instructions that performs a specific task, packaged as a unit.
The unit then can be used in programs wherever that particular task should be performed.

### Function vs Method?

Function
- **A thing that takes in parameters.**
- **Provides output that depends on these parameters**
- **Is it's own thing**

Method
- **Has to be part of class**
- **Can access external state ex. this.** 


### What is an Pure Functions?

Functions which just operate on input and they don't access external state.
Functional Programming is idea of composing code using pure functions.


### limitations of Object Oriented Programming

Object Oriented way of passing a behaviour. what you are passing is not a behaviour, 
it's an instant of an object. wouldn't it be nice to pass the behaviour itself rather 
than passing the class that has the behaviour.


### First Class Entities

You can assign a function and put it into a variable and pass it around.
Visibility of method depends on which class it belongs to and who is accessing it.
It only makes sense in context of a class.

```java
myFunction = public void doTask(){
                 System.out.println("Hello World");
             }
```

- Public is important only in the context if it is associated with a class.
Anyone who has access to myFunction as varible can run it. Therefore dropping public.

- Function name is reffered by varible name. Therefore drop method name.

- Return type is inferred. Therefore drop return type.
 
- While introducing lamda expression to the language they wanted to make sure previous version of java can use libraries which were written with lamda.

- They created a subtye of interfaces called Functional Interfaces.


```java
myFunction = () -> {
                 System.out.println("Hello World");
             }
```


## Lamda Hands On

We Execute a lamda expression by calling a method on the interface which is the
method that gave it the clue about what the expression type needs to be.

In Polymorphism we pass a thing which has different behaviour,
but in funtional programming we pass the behavour itself.

```java

interface MathOperation {

    int operation(int x);

}

interface AnotherOperation {

      int operation (int x);

}

public class LamdaExamples {
  
     public static void main (String [] args){
        
           MathOperation   = x -> x + 1;
           int result = increment.operation(10);
           System.out.println(result);                  // 11

           MathOperation newLamda = num -> num*2 + 124;
           System.out.println(newLamda.operation(20));  // 164

        // same types are assignable to each other.
           newLamda  = increment;
           System.out.println(newLamda.operation(20));  // 21

           




     }

}

```

### Changing the Imperative code to Functional using Lamda.


```java

interface Task {
    void run();
}

class HelloWorldTask implements Task {

     @Override
     public void run(){
          System.out.println();
     }

}

public class TaskRunner {

      public static void runner(Task task){
           System.out.println("Start:  " + LocalDateTime.now());
           task.run();
           System.out.println("End:  " + LocalDateTime.now());
      }


      public static void runner(Task task){
           System.out.println("Start:  " + LocalDateTime.now());
           task.run();
           System.out.println("End:  " + LocalDateTime.now());
      }

      public static void main(String [] args){
           Task task = new HelloWorldTask();
           TaskRunner.runner(task);
      }

}

```

---
---
---


```java

interface Task {
    void run();
}

public class TaskRunner {

      public static void runner(Task task) {
           System.out.println("Start:  " + LocalDateTime.now());
           task.run();
           System.out.println("End:  " + LocalDateTime.now());
      }

      public static void main(String [] args) {
//          Task task = ( ) -> System.out.println("Hello World");
//          TaskRunner.runner(task);

            TaskRunner.runner(() -> System.out.println("Hello World"));

      }

}

```

### Another Example 

```java

@FunctionalInterface
interface IntOperation {

    int doOperation(int i);

}

public class Calculator {
     
       public static int doMathOperation(IntOperation op, int a, int b){

               return op.doOperation(a, b);
       }

       public static void main( String [] args){
        
              IntOperation addition = (x, y) -> x + y;
              IntOperation subtraction = (x, y) -> x - y;
              doMathOperation(addition, 10, 20);
              doMathOperation(subtraction, 30, 20);

       }

}

```

### Lamda Vs Anonymous Inner Classes

- Difference at byte code level (creates a new instance).
- Anonymous classes trigger object creation.
- Lamdas trigger `invokedynamic` instruction.
- In javascript there in no need for fuctional interface.

```java 

public class TaskRunner {

     public static void runner(Task task) {

           System.out.println("Start: " +LocalDateTime.now());
           task.run();
           System.out.println("End: " + LocalDateTime.now());

     }

     public static void main(String [] args){
          TaskRunner.runner(
               new Task() {
                  @Override
                  public void run (){
                      System.out.println("Hello World");
                  }
               }
     }

}

```

### JDK Functional Interfaces

- Prebuilt interfaces for common lamda signatures.
- Help avoid having to create functional interfaces for every usecase.
- Reside in `java.util.functional` package
- Around 40 interfaces
- Functional Interfaces in JDK falls under certain categories

- **Functions**
- **Consumers**
- **Suppliers**
- **Predicates**

### Functions (Functional Interface)

- Takes one input
- Return one output

```java
@FunctionalInterface
public interface Function<T,R> {
     R apply(T t);
}

Function <Integer, Integer> foo = x -> x + 1;

Function <Integer, String> foo = x -> "value is " + x;

```

### Consumer (Functional Interface)

- **Takes in an arg and doesn't return anything**

```java



```

### Supplier (Functional Interface)

- **Doesn't takes any arguments but it returns something**

```java



```

### Predicate (Functional Interface)

- **Takes any arguments and resolves it to true or false**

```java



```

### Runnable (Functional Interface)

- **Takes no arguments and returns nothing**

```java
@FunctionalInterface
public interface Runnable<T,R> {
     void run();
}
```

### Examples

```java
public class JDKFUnctionInterfaceDemo {

      public static void main(String [] args){

            Function <Integer, Integer> f1 = x -> x * 2;
            f1.apply(10);  // 20 

            Function <Integer,String> f2 = x -> "Value is : " + x;
            f2.apply(10)  // Value is : 10

            Consumer <String> greeting = name -> System.out.println("Hello, " + name);
            greeting.accept("Koushik")   // Hello, Kaushik

            Supplier <Double> random = ( ) -> Math.random();
            random.get();   // Returns a Double value

            Predicate <Integer> isEven = num -> num%2 == 0;
            isEven.test(10)   // Returns true/false
            // or
            Function <Integer, Boolean> isEven = num -> (num%2) == 0;
            isEven.apply(10)  // Returns true/false

      }

}

```

### BiFucntion 

- Inorder to support binary functions there si another set of functional interfaces which have bi in prefix

```java

- Bifunction<Integer,Integer,Integer> add = (x,y) -> x + y;
- BiConsumer<String, String> printCount = (a,b) -> System.out.println(a.concat(b));
- BiPredicate<String, String> isCaseInsensitiveEqual = (a,b) -> a.equalsIgnoreCase(b);

```

### Operator

- Shortcut for Function & BiFunction.
- Takes in a type and pass the same type to rest of the types needed.

```java

UnaryOperator<Integer> increment = x -> x + 1;
//or
Function <Integer, Integer> increment = x -> x + 1;

BinaryOperator<String> concat = (a,b) -> a.concat(b);
//or
Bifunction<String,String,String> concat = (a,b) -> a.concat(b);

```

### Method References

When your lamda is just only calling another method and doing nothing else.
Then there is syntactic shortcut to avoid arg names called Methos References.

```java

//No argument is passed,lamda is just a method call
//Supplier<Double> generateRandomNumber = () -> Math.random();
  Supplier<Double> generateRandomNumber = () -> Math::random;

//Whatever input arg you provide it is just passing it around
//Consumer<String> printName = name -> System.out.println(name);
  Consumer<String> printName = System.out::println;

//UnaryOperator<String> trim = str -> str.trim();
  UnaryOperator<String> trim = String::trim;

//BiPredicate<String, String> isCaseInsensitiveEqual = (a,b) -> a.equalsIgnoreCase(b);
  BiPredicate<String, String> isCaseInsensitiveEqual = String::equalsIgnoreCase;

```

```java

public class Person {

     private String name;
     private int age;

     public Person(String name, int age){
          this.name = name;
          this.age = age;
     }

     public String getname() {
         return name;
     }

     public void setName(String name){
         this.name = name;
     }

}

public class MethodRefernceDemo {

      public static void main(String [] args){

           Function<Person, String> getName = Person::getName;

           Person p1 = new Person("Foo",25);
           Person p2 = new Person("Bar",25);

         //BiPredicate <Person,Person> isEqual = (per1,per2) -> per1.equals(per2);
           BiPredicate <Person,Person> isEqual = Person::equals;


         //It's an instance method, depends on instance passed.
         //Function<List<String>, Integer> getCount = list -> list.size();
           Function<List<String>, Integer> getCount = List::size;


         //Function<ArrayList<String>, Integer> getCount = list -> list.size();
           Function<ArrayList<String>, Integer> getCount = List::size;

         //You can use a constructor for method references as contructor is also a special method (new).
         //Create lamda which takes in a list and return deduped list
         //Function <ArrayList<String>,Collection<String>> dedupe =  list -> new HashSet<>(list);
           Function <ArrayList<String>,Collection<String>> dedupe = HashSet::new;
           

      }

}

```

### Lamdas calling lamdas calling lamdas

- Essence of functional programming
- Functions as first class entities
- Used to build composable functions


```java

public class LamdaComposibility {

/*
     public class void runner(UnaryOperator<Integer> operator) {
          System.out.println("Start: " + LocalDateTime.now());
          operator.apply(10);
          System.outprintln("End: " + LocalDateTIme.now());
     }
*/

}


public static void main(String [] args) {

     UnaryOperator<Integer> increment = x -> x + 1;

     Consumer<String> logMessage  = msg -> System.out.println(msg + ": " + LocalDateTime.now());

//   Runnable logStart = () -> System.out.println(Start: " + LocalDateTime.now());
     Runnable logStart = () -> logMessage.accept("Start");
//   Runnable logEnd = () -> System.out.println(Start: " + LocalDateTime.now());
     Runnable logStart = () -> logMessage.accept("End");
 

     BiConsumer<UnaryOperator<Integer>, Integer>(operation, number) logger -> {
//        System.out.println("Start: " + LocalDateTime.now());
          logStart.run();
          operator.apply(number);
//        System.outprintln("End: " + LocalDateTIme.now());  
          logEnd.run(); 
     };

     logger.accept(x -> x + 1, 20);
     logger.accept(x -> x*100,42);

}

```

### Composibility with andThen() and compose()

```java

Function <Integer, Integer> increment = x -> x + 1;
Function <Integer, Integer> doubleIt = x -> x * 2;

int i = 10;

//Function<Integer, Integer> combine = increment.apply(doubleIt.apply(i));
  Function<Integer, Integer> combine = increment.andThen(doubleIt);  // 21
  System.out.println(combine.apply(i));

```

### Composibility using method referneces.

```java

Function <String, String> trimLeading  = String::stripLeading;
Function <String, String> trimTrailing = String::stripTrailing;
Function <String, String> uppeCase = String::toUpperCase;

String name = "  ABCD    ";

String processedName = trimLeading
                             .andThen(trimTrailing)
                             .andThen(uppeCase)
                             .apply(name);

               //or

String processedName = trimLeading
                             .andThen(String::stripTrailing;)
                             .andThen(String::toUpperCase)
                             .apply(name);

```

### Closures in Java

- Lamdas can access variables in scope.
- But run in a completely different scope.
- What happens to the variables? Java remembers and lock the value of variables nad use it when lamda execute.
- Closures are thing when functions are first class entities.
- When a lamda is created it is going to lock all of the variable values that are within the scope of that lamda.



```java

public class ScopesProblem {

    public static Function<Integer, Integer> counter() {
     //  java says make it final or effectively final, if a varible is passed to lamda as non argumental variable
     //  int count = 0;
         final int count = 0;
         Function <Integer, Integer> increment = x -> count + 1;
     //  Compiler Error : Variable used in lamda expression should be final or effectively final  
     //  count = count + 1;  
     
         return increment;
    }

    public static void main (String [] args) {
         Function <Integer, Integer> counter = ScopesProblem.counter();
         System.out.println(counter.apply(0));    // 1
    }

}

```

### 

```java

public class ScopesProblem {

    public static Function<Integer, Integer> counter() {
    
   // You cannot change the refernce but contents of refernce associated with the reference.
      Person p = new Person();
      Function <Integer, Integer> increment = x -> p.getAge() + 1;
      p.setAge(30);      // compiler is still happy as only content has changed associated with reference.
   // p = new Person("Abhinav", 28);  // Compiler throws error
   
    }

    public static void main (String [] args) {
         Function <Integer, Integer> counter = ScopesProblem.counter();
         System.out.println(counter.apply(27));    // 28
    }

}

```

## Streams 

### Streams is a single use declarative sequential data pipelines with lazy execution

### Features of Streams Api

- Streams are a different way of dealing with collections or it is 
  another design pattern for processing elements inside a collection. 
- It's a declarative approach
- It uses lazy evaluation which makes it efficient.
- Streams api and functional programming are a match made in heaven 
  which supports composibility and parallel execution
- As a result we have optimised performance.
- Java streams are immutable.

Stream Consists of :-

- Create a Stream
- Intermediate Operation
- Terminal Operation


```java

public class IteratonDemo {

     public void examine(List<String> list, Consumer<String> operator) {
          for(String element : list){
               operation.accept(element);
          }
     }

     IterationDemo.examine(fruits, System.out::println);
}

```

### Given a collection, you can create stream out of it

```java

public class StreamDemo {

     public static void main (String [] args) {

          List <String> names = List.of("Foo","Bar","Baz");
     /*
          Stream<String> stream = names.stream();
          Consumer<String> print = str -> System.out::println;

          stream.forEach(print)     // forEach takes in a Consumer as argument
     */

          Stream<String> stream = names.stream();
          stream.forEach(System.out::println);         
     }

}

```

### Other ways to create stream

```java

public class StreamDemo {

     public static void main (String [] args) {

          Set <String> names = Set.of("Foo","Bar","Baz");

          Stream<String> stream = names.stream();
          stream.forEach(System.out::println);         
     }

}

```

### Other ways to create stream (From Arrays)

```java

public class StreamDemo {

     public static void main (String [] args) {
       
         int [] numbers = {1,2,3,4,5,6};

         Arrays.stream(numbers).forEach(System.out::println);
       
     }

}

```

### Other ways to create stream (Using Stream.of())

```java

public class StreamDemo {

     public static void main (String [] args) {
       
           Stream.of("mango","apple","banana").forEach(System.out::println);
       
     }

}

```

### Create a stream from every line of a file (Using built in APIs that return stream)

```java

public class StreamDemo {

     public static void main (String [] args throws IOException) {
     
          Stream<String> lines = Files.lines(Paths.get("README.md")); // Return stream of string
          lines.forEach(System.out::println);

     }
}

```

### Create a infinite stream and limit it using a supplier.

```java

public class StreamDemo {

     public static void main (String [] args throws IOException) {
     
//          Stream.generate(Math::random);
            Stream.generate(new Random()::nextDouble)
                  .limit(10)
                  .forEach(System.out::println);

     }
}

```

### Create a stream of even numbers with iterate()

```java

public class StreamDemo {

     public static void main (String [] args throws IOException) {
     
          // give a starting point & give a finction to get next value
          // 0 , x -> x + 2 = 2
          // 2 , x -> x + 2 = 4
          // ...  
          //0 2 4 6 8
          Stream.iterate(0,x -> x + 2)
               .limit(10)
               .(forEach());
     }
     
}

```

### Create a collection out of stream

```java

public class StreamDemo {

     public static void main (String [] args throws IOException) {
     
          List<Integer> upToHundred = Stream.iterate(0, x -> x + 1)
                 .limit(100)
                 .toList();

          System.out.println(upToHundred);
     }
     
}

```

### Collections Vs Streams

- **Immutability** Collections are mutable, streams are not.
- **Laziness** Collections operations are eager, strems are lazy
- **Processing Intent**  Collection focus on storing, streams on processing and transforming.
- **Parallelism** Collections are agnostic, while streams support it.

### Limit & Filter Operation

### limit()

```java

public class IntermediateOperations {

      public static void main (String [] args) {
           
//         Stream <Integer> numbers = Stream.of(1,2,3,4,5,6,7,8,9,10);

//         Stream<Integer> anotherStream  = numbers.limit(5);  // results in another stream.
//         anotherStream.forEach(System.out::println);

//         numbers.limit(5).forEach(System.out::println);

           Stream.of(1,2,3,4,5,6,7,8,9,10)
                 .limit(5)                       // creates another stream
                 .forEach(System.out::println);     

      }
}

```

### filter() -> creates a new stream

```java

public class IntermediateOperations {

      public static void main (String [] args) {
/*           
           Stream <Integer> numbers = Stream.of(1,2,3,4,5,6,7,8,9,10);          
           Stream<Integer> evenStream = numbers.filter(x -> x % 2 == 0);  // takes in predicate
           evenStream.forEach(System.out::println);
*/
           Stream.of(1,2,3,4,5,6,7,8,9,10)
                 .filter(x -> x % 2 == 0)
                 .forEach(System.out::println);     

      }
}

```

### filter() + limit()

```java

public class IntermediateOperations {

      public static void main (String [] args) {
/*           
           Stream <Integer> numbers = Stream.of(1,2,3,4,5,6,7,8,9,10);          
           Stream<Integer> evenStream = numbers.filter(x -> x % 2 == 0);  // takes in predicate
           Stream<Integer> firstTwoEven = evenStream.limit(2);
           firstTwoEven.forEach(System.out::println);
*/
           Stream.of(1,2,3,4,5,6,7,8,9,10)
                 .filter(x -> x % 2 == 0)
                 .limit(2)
                 .forEach(System.out::println);     

      }
}

```

### map() -> allows you to change the element and put it into new stream

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<String> names =  Stream.of("apple","banana","mango","strawberry");
           names.map(String::toUpperCase).forEach(System.out::println);

           //Print only first two fruits
           names
                .map(String::toUpperCase)
                .limit(2)
                .forEach(System.out::println);

      }
}

```

### Remove anything that is greater than 6 char using map()

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<String> names =  Stream.of("apple","banana","mango","strawberry");
           names
               .map(String::toUpperCase)
               .filter(name -> name.length() < 6)
               .forEach(System.out::println);

      }
}

```

### Inroder to examine a stream in between use peek() -> takes in a consumer and return a stream

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<String> names =  Stream.of("apple","banana","mango","strawberry");
           names
               .map(String::toUpperCase)
               .peek(str -> System.out.println("Peek result: " + str))
               .filter(name -> name.length() < 6)
               .forEach(System.out::println);

      }
}

```

### Diff b/w peek() & forEach()

- forEach() is a terminal/final operation
- peek() is an intermediate operation


### Streams Api are lazy 

- They work only if there is someone to consume the result of their work.

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<String> names =  Stream.of("apple","banana","mango","strawberry");
           names
               .map(String::toUpperCase)
               .peek(str -> System.out.println("Peek result: " + str))  // peek() will not work as streams are lazy
               .filter(name -> name.length() < 6)
               // There has to be a terminal operation to consume its work.

      }
}

```

### distinct() operator

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<String> numbers =  Stream.of(1,2,2,3,3,3,1,3,5,6,7,2,4,5,6,7);
           numbers
               .peek(num -> System.out.println("Peek result: " + num))
               .distinct()
               .forEach(System.out::println);
      }
}

```

### sorted() operator

- intermediate operation
- returns a new stream
- sorted according to natural order (for 'Comparable') or using a provide Comparator
- for large streams, sorting can be time taking
- for infinite streams, it will never complete (kills memory)

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<Integer> numbers =  Stream.of(1,2,2,3,3,3,1,3,5,6,7,2,4,5,6,7);
           numbers
               .peek(num -> System.out.println("Peek result: " + num))
               .distinct()
               .sorted()
               .forEach(System.out::println);
      }
}

```

### Concatenate two streams

```java

public class IntermediateOperations {

      public static void main (String [] args) {

           Stream<Integer> oddNumbers =  Stream.of(1,3,5,7);
           Stream<Integer> evenNumbers = Stream.of(2,4,6,8);
           Stream.concat(oddNumbers, evenNumbers).forEach(System.out::println); // print all odd and then even

      }
}

```