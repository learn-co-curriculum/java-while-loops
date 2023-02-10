# While Loops

## Learning Goals

- Define what a `while` loop is.
- Show how to implement a `while` loop and how it differs from the `for` loop.

## What is a `while` Loop?

A `while` loop is another way to iterate through a section of code multiple
times based on a boolean expression. When the conditional is true, then the code
will continuously be executed until the condition becomes false. The syntax for
a `while` loop is as follows:

```java
while (conditional) {
    // Statements to run through each iteration of the loop
}
```

This kind of loop is well suited in cases where we do not know how many times we
want to go through a specific set of instructions. Consider the following
flowchart:

![while-loop-flowchart](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/while-loop-flowchart.png)

## While Loop in Action

Let's consider some code where we want to keep a running sum of the positive
integers entered by a user.

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class LoopExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Running sum of integers
        int sum = 0;
        
        try {
            System.out.println("Please enter a positive integer:");
            System.out.println("Program will end when a non-positive integer is entered.");
            int userNumber = scanner.nextInt();
            
            while (userNumber >= 0) {
                // Only add positive integers
                sum += userNumber;

                System.out.println("Please enter a positive integer:");
                userNumber = scanner.nextInt();
            }
            
            System.out.println("The sum of the numbers you entered is: " + sum);
            
        } catch (InputMismatchException exception) {
            System.out.println("Invalid input");
        }
    }
}
```

Let's break down what this `while` loop does:

- If the user enters an integer that satisfies the conditional
  `userNumber >= 0`, then the execution will enter the `while` loop. Else, the
  execution will skip over the `while` loop.
- It will execute the statements inside the `while` loop and then check the
  condition again to see if it should re-enter the loop.
- Notice how we prompt the user again in the `while` loop as well. This is so
  we can continue checking to see if the conditional is true.
  - In this case, we can refer to the `userNumber` variable as a
    **sentinel value**. A sentinel value is a value that is used to terminate a
    loop and stop getting inputs. It serves as the exit out of the `while` loop.
    In our example, it also indicates that the user is done entering values.

If we run the program with the following input:

```text
1
2
3
-1
```

The output would look like this:

```text
Please enter a positive integer:
Program will end when a non-positive integer is entered.
1
Please enter a positive integer:
2
Please enter a positive integer:
3
Please enter a positive integer:
-1
The sum of the numbers you entered is: 6
```

We can take a closer look at this program by running it in the debugger and
analyzing each iteration.

We'll set two breakpoints:

- On the `while (userNumber >= 0)` line.
- On the `System.out.println("The sum of the numbers you entered is: " + sum);`

For the first number, we'll enter the integer `1`:

![hit-breakpoint](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-hit-breakpoint-5.png)

Notice that the `userNumber` variable has the value of `1`. Since the
conditional is `userNumber >= 0`, we can evaluate that expression to `1 >= 0`,
which is `true`. So, if we use the step-over action, we should enter in the
`while` loop:

![enter-while-loop](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-enter-while-loop.png)

Now that we are in the loop, Java will continue executing all the statements
within the loop. If we resume the program and enter in `2` this time, we should
hit the `while` loop breakpoint again:

![hit-while-loop-condition-again](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-hit-breakpoint-6.png)

The `userNumber` variable has been reassigned to the value of `2`; therefore,
the condition `userNumber >= 0` is equivalent to `2 >= 0`, which is still
`true`. We can step-over the action and see it enter the loop again.

![enter-while-loop-second-iteration](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-enter-while-loop-2.png)

Just like last time, Java will continue executing all the statements in the
`while` loop. Let's resume the program and enter in `-1` this time:

![hit-while-loop-condition-third-time](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-hit-breakpoint-7.png)

Notice we hit the `while` loop breakpoint again! We'll check the condition again
to see if we should re-enter the loop. `userNumber` has been reassigned to `-1`,
so the condition `userNumber >= 0` is equivalent to `-1 >= 0`. This time, the
condition is `false`, so Java should exit the loop and proceed with executing
the statements that follow the `while` loop. Let's step-over and see if this is
what happens:

![exit-while-loop](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-debugger-exit-while-loop.png)

We can resume the program and see that the output this time is now:

```text
Please enter a positive integer:
Program will end when a non-positive integer is entered.
1
Please enter a positive integer:
2
Please enter a positive integer:
-1
The sum of the numbers you entered is: 3
```

## Infinite Loops

Consider the following code:

```java
while (true) {
    System.out.println("I'm a loop that never ends, aka an infinite loop");
}
```

In the code above, the statement
`System.out.println("I'm a loop that never ends, aka an infinite loop");` will
run as long as the condition specified in the `while` loop evaluates to
`true`. Since that condition is literally the `boolean` value `true`, the
condition will always be true and the loop will never stop executing. This is
an **infinite loop**, and although useful in some specific rare cases, it
generally leads to **bugs** or issues within the code.

Let's look at another infinite loop example:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class LoopExample {
   public static void main(String[] args) {
      Scanner scanner = new Scanner(System.in);

      // Running sum of integers
      int sum = 0;

      try {
         System.out.println("Please enter a positive integer:");
         System.out.println("Program will end when a non-positive integer is entered.");
         int userNumber = scanner.nextInt();

         while (userNumber >= 0) {
            // Only add positive integers
            sum += userNumber;
            
            // Removed the updating of userNumber
         }

         System.out.println("The sum of the numbers you entered is: " + sum);

      } catch (InputMismatchException exception) {
         System.out.println("Invalid input");
      }
   }
}
```

Notice we have removed the reassignment statement of `userNumber` from within
the `while` loop itself. In this case, if the user were to enter a positive
integer, we would be stuck in an infinite loop without updating the sentinel
value!

If we were to run this program and enter in a value of `2`, the program would
just sit there. It would look like it is doing nothing since we have no
`System.out.println()` statements within the loop itself. When this happens, we
need to manually stop and exit the program by clicking on the stop button in the
upper-right hand corner of Intellij:

![stop-button](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-stop-button.png)

This demonstrates the importance of the sentinel value when working with loops.
It should also be noted that IntelliJ does try to warn us of infinite loop bugs
as well:

![infinite-loop-warning](https://curriculum-content.s3.amazonaws.com/java-mod-1/while-loops/intellij-infinite-loop-warning.png)
