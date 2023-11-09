# 📚Clean Code: A Handbook of Agile Software Craftsmanship📚

Welcome to the programmer's guide to "Clean Code" by Robert C. Martin🚀

## About the Book 📖

Even bad code can function. But if code isn’t clean, it can bring a development organization to its knees. Every year, countless hours and significant resources are lost because of poorly written code. But it doesn’t have to be that way.🌌

Clean Code is divided into three parts. The first describes the principles, patterns, and practices of writing clean code. The second part consists of several case studies of increasing complexity. Each case study is an exercise in cleaning up code—of transforming a code base that has some problems into one that is sound and efficient. The third part is the payoff: a single chapter containing a list of heuristics and “smells” gathered while creating the case studies. The result is a knowledge base that describes the way we think when we write, read, and clean code.🌌

## Chapter 1: Clean Code 🌅
*Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer's intent but rather is full of crisp abstractions and straightforward lines of control.*

*Books on art don't promise to make you an artist. All they can do is give you some of the tools, techniques, and thought processes that other artists have used. So too this book cannot promise to make you a good programmer. It cannot promise to give you "code-sense.?" All it can do is show you the thought processes of good programmers and the tricks, techniques, and tools that they use.
Just like a book on art, this book will be full of details. There will be lots of code.
You'll see good code and you'll see bad code. You'll see bad code transformed into good code. You'll see lists of heuristics, disciplines, and techniques. You'll see example after example. After that, it's up to you.*

- Grady Booch, author of Object Oriented Analysis and Design with Applications

> The first chapter delves into the perspectives of industry celebrities as they discuss what clean code means to them. The comparison of clean code to well-written prose stood out to me due to my background in English literature. In a story, there is a beginning, a middle, and an end, filled with ups and downs. Similarly, a local variable in a program, too, goes on a journey It is up to the writer to communicate with the reader in meaningful ways.

## Chapter 2: Meaningful Names 🔍
**Variables with unclear context**
``` java
private void printGuessStatistics(char candidate, int count) {   String number;
       String verb;
       String pluralModifier;
       if (count == 0) {
         number = ”no”;
         verb = ”are”;
         pluralModifier = ”s”;
       } else if (count == 1) {
         number = ”1”;
         verb = ”is”;
         pluralModifier = ””;
       } else {
         number = Integer.toString(count);
         verb = ”are”;
         pluralModifier = ”s”;
       }
       String guessMessage = String.format(
         ”There %s %s %s%s”, verb, number, candidate, pluralModifier
       );
       print(guessMessage);
     }
```
**Variables have a context**
``` java
public class GuessStatisticsMessage {
     private String number;
     private String verb;
     private String pluralModifier;

     public String make(char candidate, int count) {
       createPluralDependentMessageParts(count);
        return String.format(
          "There %s %s %s%s", 
          verb, number, candidate, pluralModifier );
     }

     private void createPluralDependentMessageParts(int count) {
       if (count == 0) {
         thereAreNoLetters();
       } else if (count == 1) {
         thereIsOneLetter();
       } else {
         thereAreManyLetters(count);
       }
     }

     private void thereAreManyLetters(int count) {
       number = Integer.toString(count);
       verb = "are";
       pluralModifier = "s";
     }

     private void thereIsOneLetter() {
       number = "1";
       verb = "is";
       pluralModifier = "";
     }

     private void thereAreNoLetters() {
       number = "no";
       verb = "are";
       pluralModifier = "s";
     }
   }
```
> Encapsulation and Modularity: GuessStatisticsMessage encapsulates the logic within separate methods (thereAreManyLetters, thereIsOneLetter, thereAreNoLetters) for different cases, making the code modular and easier to read. Each method handles a specific case, improving the code's readability and maintainability.

> Reusability: The logic for creating the message parts (number, verb, pluralModifier) is encapsulated within private methods. This allows for easy reuse of the logic in other parts of the code or in different methods, promoting the DRY (Don't Repeat Yourself) principle.

> Overall, the GuessStatisticsMessage class follows an object-oriented approach, allowing for better organization of code, data, and behavior. This approach aligns with principles like encapsulation and abstraction, making the codebase more maintainable and extensible in the long run.

## Chapter 3: Functions 🚶‍♂️

**FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.**

✏️ *[One] way to know that a function is doing ‘one thing’ is if you can extract another function from it with a name that is not merely a restatement of its implementation* 

✏️ *One level of abstraction per function*
> A function call is a high-level of abstraction, whereas buffer.append(“\n”) is a low-level of abstraction.

✏️ *Don’t be afraid to make a [function] name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment*

✏️ *Function Arguments*

A:
``` java
writeField(name);

// is better than:

write(name);
```
B:
``` java
assertExpectedEqualsActual (expected, actual)
```
> This naming convention strongly mitigates the problem of having to remember the ordering of arguments.

✏️ *Either your function should change the state of an object, or it should return some information about that object*

Don't do this:
``` java
Public boolean set (String attribute, String value);
// Returns true/false and “sets”

// Solution
If (attributeExists (“username”)) {
setAttribute (“username”, “unclebob”);
…
	}
```

*The art of programming is, and has always been,* ***the art of language design.***

*Master programmers think of systems as stories to be told rather than programs to be written. They use the facilities of their chosen programming language to construct a much richer and more expressive language that can be used to tell that story. Part of that domain-specific language is the hierarchy of functions that describe all the actions that take place within that system. In an artful act of recursion those actions are written to use the very domain-specific language they define to tell their own small part of the story.*

*This chapter has been about the mechanics of writing functions well. If you follow the rules herein, your functions will be short, well named, and nicely organized. But never forget that your real goal is to tell the story of the system, and that the functions you write need to fit cleanly together into a clear and precise language to help you with that telling.*

## Chapter 4: Comments 🤝
✏️ Comments Do Not Make Up for Bad Code

*One of the more common motivations for writing comments is bad code. We write a module and we know it is confusing and disorganized. We know it’s a mess. So we say to ourselves, “Ooh, I’d better comment that!” No! You’d better clean it!*

✏️ Explain Yourself in Code

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) &&
       (employee.age > 65)) {
…
}
// Recfactored, minus comment
if (employee.isEligibleForFullBenefits()) {
…
}
```
*It takes only a few seconds of thought to explain most of your intent in code. In many cases it’s simply a matter of creating a function that says the same thing as the comment you want to write.*

✏️ Don’t Use a Comment When You Can Use a Function or a Variable
```java
// does the module from the global list <mod> depend on the subsystem we are part of?
   if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))

// This could be rephrased without the comment as
   ArrayList moduleDependees = smodule.getDependSubsystems();
   String ourSubSystem = subSysMod.getSubSystem();
   if (moduleDependees.contains(ourSubSystem))
```
*The author of the original code may have written the comment first (unlikely) and then written the code to fulfill the comment. However, the author should then have refactored the code, as I did, so that the comment could be removed.*

✏️ Nonlocal Information

*If you must write a comment, then make sure it describes the code it appears near. Don’t offer systemwide information in the context of a local comment. Consider, for example, the javadoc comment below. Aside from the fact that it is horribly redundant, it also offers information about the default port. And yet the function has absolutely no control over what that default is. The comment is not describing the function, but some other, far distant part of the system. Of course there is no guarantee that this comment will be changed when the code containing the default is changed.*

```java
   /**
    * Port on which fitnesse would run. Defaults to 8082.
    *
    * @param fitnessePort
    */
   public void setFitnessePort(int fitnessePort)
   {
     this.fitnessePort = fitnessePort;
   }
```

## Chapter 5: Formatting 🔮
✏️ The Purpose of Formatting

*Perhaps you thought that “getting it working” was the first order of business for a professional developer. I hope by now, however, that this book has disabused you of that idea. The functionality that you create today has a good chance of changing in the next release, but the readability of your code will have a profound effect on all the changes that will ever be made. The coding style and readability set precedents that continue to affect maintainability and extensibility long after the original code has been changed beyond recognition. Your style and discipline survives, even though your code does not.*

✏️ Indentation 

*A source file is a hierarchy rather like an outline. There is information that pertains to the file as a whole, to the individual classes within the file, to the methods within the classes, to the blocks within the methods, and recursively to the blocks within the blocks. Each level of this hierarchy is a scope into which names can be declared and in which declarations and executable statements are interpreted.*

*To make this hierarchy of scopes visible, we indent the lines of source code in proportion to their position in the hiearchy.*

*Programmers rely heavily on this indentation scheme. They visually line up lines on the left to see what scope they appear in. This allows them to quickly hop over scopes, such as implementations of if or while statements, that are not relevant to their current situation. They scan the left for new method declarations, new variables, and even new classes. Without indentation, programs would be virtually unreadable by humans.*

> EXAMPLE
```java
public class FitNesseServer implements SocketServer { private FitNesseContext 
   context; public FitNesseServer(FitNesseContext context) { this.context = 
   context; } public void serve(Socket s) { serve(s, 10000); } public void 
   serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new 
   FitNesseExpediter(s, context); 
   sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); } 
   catch(Exception e) { e.printStackTrace(); } } }
```

> VERSUS

```java
   public class FitNesseServer implements SocketServer {
     private FitNesseContext context;

     public FitNesseServer(FitNesseContext context) {
       this.context = context;
     }

     public void serve(Socket s) {
       serve(s, 10000);
     }

     public void serve(Socket s, long requestTimeout) {
       try {
         FitNesseExpediter sender = new FitNesseExpediter(s, context);
         sender.setRequestParsingTimeLimit(requestTimeout);
         sender.start();
       }
       catch (Exception e) {
         e.printStackTrace();
       }
    }
  }
```
## Chapter 6: Objects and Data Structures 💫

*Objects hide their data behind abstractions and expose functions that operate on that data. Data structure expose their data and have no meaningful functions.*

*Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes it hard to add new behaviors to existing objects. Data structures expose data and have no significant behavior. This makes it easy to add new behaviors to existing data structures but makes it hard to add new data structures to existing functions.*

*In any given system we will sometimes want the flexibility to add new data types, and so we prefer objects for that part of the system. Other times we will want the flexibility to add new behaviors, and so in that part of the system we prefer data types and procedures. Good software developers understand these issues without prejudice and choose the approach that is best for the job at hand.*

✏️ The Law of Demeter

*There is a well-known heuristic called the Law of Demeter that says a module should not know about the innards of the objects it manipulates.*

*This means that an object should not expose its internal structure through accessors because to do so is to expose, rather than to hide, its internal structure. The method should not invoke methods on objects that are returned by any of the allowed functions. In other words, talk to friends, not to strangers.*

> More on **The Law of Demeter** : an object should only communicate with its immediate neighbors and should not have knowledge of the internal details of other objects. This promotes encapsulation and reduces dependencies between classes, leading to more maintainable and flexible code.  The idea is to minimize the number of relationships an object has with other objects and to keep interactions as local as possible to reduce coupling and maintain encapsulation.

> EXAMPLE
```java
class PaymentProcessor {
    public void processPayment(double amount) {
        // Logic for processing payment
        System.out.println("Payment processed: $" + amount);
    }
}

class Wallet {
    private PaymentProcessor paymentProcessor;

    public Wallet() {
        this.paymentProcessor = new PaymentProcessor();
    }

    public void makePayment(double amount) {
        // Delegate payment processing to PaymentProcessor
        paymentProcessor.processPayment(amount);
    }
}

class Customer {
    private Wallet wallet;

    public Customer() {
        this.wallet = new Wallet();
    }

    public void purchaseItem(double amount) {
        // Customer makes a payment through the wallet
        wallet.makePayment(amount);
    }
}

public class Main {
    public static void main(String[] args) {
        Customer customer = new Customer();
        double itemPrice = 50.0;
        customer.purchaseItem(itemPrice);
    }
}
```

> The Wallet class is considered an immediate neighbor of the Customer class because it represents an intermediate level of abstraction between the Customer and the PaymentProcessor. The Customer class directly interacts with the Wallet class, and the Wallet class, in turn, interacts with the PaymentProcessor.

> By introducing this intermediate level of abstraction, the Customer class adheres to **the Law of Demeter** by delegating the payment processing responsibility to the Wallet class. This encapsulates the payment processing logic within the Wallet class and allows the Customer class to remain ignorant of the internal details of the PaymentProcessor. It also provides a clear and maintainable structure for managing payment-related functionality within the system.

> **1 level of abstraction = Customer -> 2 level of abstraction (neighbor) = Wallet -> 3 level of abstraction = paymentProcessing.**

> The key principle of **the Law of Demeter** is to limit the exposure of an object's internal structure to the outside world, and the Wallet class helps achieve that by serving as a mediator between the Customer and the PaymentProcessor.

## Chapter 7: Boundaries 🏰 
✏️ Using Third-Party Code

*If our application needs a Map of Sensors, you might find the sensors set up like this:*
```java
Map<Sensor> sensors = new HashMap<Sensor>();

   …

       Sensor s = sensors.get(sensorId );
```

*[However] passing an instance of Map<Sensor> liberally around the system means that there will be a lot of places to fix if the interface to Map ever changes. Indeed, we’ve seen systems that are inhibited from using generics because of the sheer magnitude of changes needed to make up for the liberal use of Maps.*

*A cleaner way to use Map might look like the following. No user of Sensors would care one bit if generics were used or not. That choice has become (and always should be) an implementation detail.*
```java
public class Sensors {

     private Map sensors = new HashMap();


     public Sensor getById(String id) {

       return (Sensor) sensors.get(id);

     }

     //snip

   }
```

*The interface at the boundary (Map) is hidden. It is able to evolve with very little impact on the rest of the application.*

*This interface is also tailored and constrained to meet the needs of the application. It results in code that is easier to understand and harder to misuse. The Sensors class can enforce design and business rules.*
> MAP functionality is abstrated away into a class - safer to use, harder to misue.

*If you use a boundary interface like Map, keep it inside the class, or close family of classes, where it is used. Avoid returning it from, or accepting it as an argument to public APIs.*

### Chapter 8: The Battle of Elements ⚔️✏️ 
A fierce battle erupts, pitting elemental forces against each other in a struggle for dominance.

### Chapter 9: The Power Within 🌟
Harnessing newfound abilities, our hero embarks on a quest for self-discovery and enlightenment.

### Chapter 10: The Tangled Web 🕸️✏️ 
Intrigue and deception weave a web of lies, challenging our protagonist's wit and intellect.

### Chapter 11: The Triumph of Goodness ✨✏️ 
Goodness prevails over darkness as the hero's actions inspire hope and ignite a revolution.

### Chapter 12: The Final Confrontation 🏹✏️ 
The ultimate showdown unfolds, testing the hero's resolve and the strength of their friendships.

### Chapter 13: The Unraveling Truth 📜✏️ 
Secrets are revealed, reshaping perceptions and leading to a profound understanding of the world.

### Chapter 14: The Journey's End 🌄
As the journey concludes, our hero reflects on lessons learned and the transformative power of knowledge.

### Chapter 15: The New Beginning 🌱
A new chapter begins, promising fresh adventures and endless possibilities for the future.

## Code Examples 💻

```java
public class FactorialCalculator {

    // Recursive function to calculate factorial
    public static int factorial(int n) {
        if (n == 0 || n == 1) {
            return 1;
        } else {
            return n * factorial(n - 1);
        }
    }
    public static void main(String[] args) {
        int number = 5; // Change this number to calculate the factorial for a different value
        int result = factorial(number);
        System.out.println("Factorial of " + number + " is: " + result);
    }
}
```

