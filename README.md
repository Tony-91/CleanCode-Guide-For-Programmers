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

### Chapter 4: The Unexpected Alliance 🤝
Unlikely allies join forces, combining their unique strengths to overcome a common adversary.

### Chapter 5: The Dark Prophecy 🔮
A prophecy looms large, foretelling a great calamity that threatens the existence of the entire realm.

### Chapter 6: The Code of Honor 💫
The hero learns the importance of integrity and honor, facing moral dilemmas that shape their destiny.

### Chapter 7: The Hidden Sanctuary 🏰
Discovering a hidden sanctuary, our protagonist unearths ancient manuscripts containing cryptic knowledge.

### Chapter 8: The Battle of Elements ⚔️
A fierce battle erupts, pitting elemental forces against each other in a struggle for dominance.

### Chapter 9: The Power Within 🌟
Harnessing newfound abilities, our hero embarks on a quest for self-discovery and enlightenment.

### Chapter 10: The Tangled Web 🕸️
Intrigue and deception weave a web of lies, challenging our protagonist's wit and intellect.

### Chapter 11: The Triumph of Goodness ✨
Goodness prevails over darkness as the hero's actions inspire hope and ignite a revolution.

### Chapter 12: The Final Confrontation 🏹
The ultimate showdown unfolds, testing the hero's resolve and the strength of their friendships.

### Chapter 13: The Unraveling Truth 📜
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

