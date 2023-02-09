# While Loops

## Learning Goals

- Define what a `while` loop is and how to implement it

## The while Statement in Java

With the `if` statement, we saw that we can make the execution of a block of
code conditional based on the outcome of a conditional statement. In that
scenario, the conditional block of code gets executed exactly once. What if we
wanted to execute the same block of code multiple times, as long as a condition
stays true? That is where the while loop comes in handy!

A **while loop** is a control flow statement where code can continuously be
executed repetitively based on a boolean expression. When the boolean
expression is true, then the code will continuously be repeated until the
expression becomes false.

```java
while (true) {
    System.out.println("I'm a loop that never ends, aka an infinite loop");
}
```

In the code above, the statement
`System.out.println("I'm a loop that never ends, aka an infinite loop");` will
run as long as the condition specified in the `while` loop evaluates to
true. Since that condition is literally the `boolean` value `true`, the
condition will always be true and the loop will never stop executing. This is
an **infinite loop**, and although useful in some specific cases, it generally
leads to **bugs** or issues within the code.

Let's consider code where the content of the `while` loop actually changes the
condition:

```java
// simulate the passing of time
int startingYear = 2000;
int targetYear = 2011;
int currentYear = startingYear;
while (currentYear < targetYear) {
    int yearDifference = currentYear - startingYear;
    System.out.println(yearDifference + " year(s) have passed");
    // conditional logic based on the current year
    currentYear++;
}
```

In this code, we can see that the condition is now an actual expression:
`currentYear < targetYear`. Furthermore, since we change the value of the
variable inside the `while` loop, the value of the condition will change with
every iteration through the loop, which means that it's possible, although not
guaranteed, that the condition will eventually become `false` and the loop will
stop executing.

Let's see what happens when we run this code!

```java
0 year(s) have passed
1 year(s) have passed
2 year(s) have passed
3 year(s) have passed
4 year(s) have passed
5 year(s) have passed
6 year(s) have passed
7 year(s) have passed
8 year(s) have passed
9 year(s) have passed
10 year(s) have passed
```

Notice that the output prints out the numbers 0 - 10. Let's walk through a
little more on what happened here:

Before we even get into the `while` loop, initialize `startingYear` and
`targetYear` to 2000 and 2011 respectively. Then we set `currentYear`
equal to `startingYear`. This means that we start with `currentYear`
being 2000.

Now we will execute the first iteration of the while loop:

1. We check the condition to see if `currentYear < targetYear`. This expression
   evaluates to 2000 < 2011; which is true. So we will enter the `while` loop.
2. We perform the difference between `currentYear` and `startingYear` and store
   the return value in the local variable `yearDifference`. So 2000 - 2000 = 0.
3. `yearDifference` is currently assigned the value of 0 and we will print that
   out on a new line.
4. Increment `currentYear`. So `currentYear++` will reassign `currentYear`
   to 2001.

In the second iteration:

1. We check the condition to see if `currentYear < targetYear`. This expression
   evaluates to 2001 < 2011; which is true. So we will continue in the
   `while` loop.
2. We evaluate the expression `currentYear - startingYear`. So 2001 - 2000 = 1.
3. Print out the value of `yearDifference`, so 1.
4. Increment `currentYear`. So `currentYear++` will reassign `currentYear`
   to 2002.

This goes on until `currentYear` is set to 2011, at which point the condition
`currentYear < targetYear` will be false. Once the boolean expression that is
controlling the `while` loop  is no longer true, we will exit the loop.
