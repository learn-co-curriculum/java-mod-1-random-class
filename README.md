# Random Class

## Learning Goals

- Learn about the Java `Random` class

## Introduction

Java has yet another class to help generate random numbers a little easier
called the `Random` class!

The **Random Class** is part of the package `java.util` and contains methods to
generate different types of random numbers. To use the `Random` class, we must
import it using the `import` statement like we saw in the Packages lesson:

```java
import java.util.Random;
```

Notice we didn't have to import the Math class in the previous lesson. This is
because the Math class is available in the `java.lang` package. If we remember
from the Packages lesson, we do not need to import the `java.lang` package
since it is in the default package.

Once we have imported the `Random` class, we can use it anywhere in our class by
instantiating an object of that type:

```java
Random random = new Random();
```

Now that we have instantiated our `Random` instance, let's put it to use by
using some of its methods!

## `nextBoolean()`

If we want a random `boolean` value, we can use the `Random` class' method
`nextBoolean()` to return a pseudorandom `boolean` value of true or false. For
example, this could be useful if we want to simulate flipping a coin and knowing
if the coin lands on heads or tails.

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        // If flipCoin() returns true, then the coin landed on heads
        if (flipCoin()) {
            System.out.println("Landed on heads");
        } else {
            System.out.println("Landed on tails");
        }
    }

    /**
     * Simulate flipping a coin.
     * If it returns true, it lands on heads; else it lands on tails
     * @return boolean - true if it lands on heads and tails otherwise
     */
    public static boolean flipCoin() {
        Random random = new Random();
        return random.nextBoolean();
    }
}
```

If we were to run this program four times, a potential output of the code above
could look like this:

```plaintext
Landed on heads
Landed on tails
Landed on tails
Landed on heads
```

## `nextDouble()` and `nextFloat()`

Like the `Math.random()` method, the `Random` class' `nextDouble()` method
returns a pseudorandom `double` value between 0.0 and 1.0.

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        Random random = new Random();
        double randomDouble = random.nextDouble();
        
        System.out.println("The random double is " + randomDouble);
    }
}
```

The `randomDouble` variable will be assigned to a different random number each
time the code is run. A potential output could look like this:

```plaintext
The random double is 0.751633395843345
```

Similarly, the `nextFloat()` method in the `Random` class returns a `float`
value between 0.0 and 1.0.

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        Random random = new Random();
        float randomFloat = random.nextFloat();
        
        System.out.println("The random float is " + randomFloat);
    }
}
```

The output of the above code could look like this:

```plaintext
The random float is 0.17982453
```

## `nextLong()`

We can also generate a random `long` value by invoking the `Random` class'
`nextLong()` method. The `nextLong()` method will return a pseudorandom `long`
value:

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        Random random = new Random();
        long randomLong = random.nextLong();
        
        System.out.println("The random long is " + randomLong);
    }
}
```

Unlike the `nextDouble()` and `nextFloat()` methods, the `nextLong()` method
does not have a bound to it. It could return both positive and negative numbers.
Consider the output if we were to execute the code above three times:

```plaintext
The random long is -3648376578569420679
The random long is 5753346489764395447
The random long is -9107496281823218113
```

## `nextInt()`

One of the most useful methods built into the `Random` class is the `nextInt()`
method. There are actually two methods of the `nextInt()` method within the
class too: One does not take in any arguments and the other one does.

The `nextInt()` method that does not take any parameters at all will simply
return a random `int` value in a similar fashion to how the `nextLong()` method
operated. This means it could return either a positive or a negative value as
long as it fits within an `int` data type:

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        Random random = new Random();
        int randomInt = random.nextInt();
        
        System.out.println("The random int is " + randomInt);
    }
}
```

If we were to execute the code above three times, we might end up with an output
like this:

```plaintext
The random int is -899314034
The random int is 959478064
The random int is 715451550
```

The other method looks like this: `nextInt(int bound)` where it takes in an
`int` as an argument. What this method will do is it returns a pseudorandom
`int` value greater than or equal to 0 and less than the `bound` specified. For
example, if we want to generate random integers between 0 and 6 inclusively, we
could write something like this:

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        Random random = new Random();
        
        /*Generate random integers between 0 - 6 inclusively
        This means we have to pass bound + 1 to the nextInt()*/
        int randomInt = random.nextInt(7);
        
        System.out.println("The random int is " + randomInt);
    }
}
```

The above could potentially have the following output:

```plaintext
The random int is 5
```

Let's go back to our die roll example again. A die has numbers 1-6 on each of
its faces. But the `nextInt(int bound)` method states that it has a lower bound
of 0. How can we force the range to be 1-6 instead of 0-6?

The answer is to take the range the same way we did with the `Math.random()`
method!

```java
import java.util.Random;

public class RandomExample {
    public static void main(String[] args) {
        System.out.println("Look! We rolled a " + rollDie());
    }

    /**
     * Model rolling a die
     * @return int - returns the face-up value the die landed on
     */
    public static int rollDie() {
        Random random = new Random();
        
        // Calculate the range
        int min = 1;
        int max = 6;
        int range = (max - min) + 1;
        
        // Generate random number between 1 and 6
        return random.nextInt(range) + min;
    }
}
```

Like we did in the Type Casting lesson, we hardcoded the numbers 1 and 6 to
define the range of a standard die. Then we did a little math to ensure that a
value between 1 and 6 is returned. Since we are using the `nextInt()` method,
we do not have to cast it to an `int` like we did with the `Math.random()`
method since `nextInt()` already returns an integer value.

Now if we were to run this program four times, a potential output of the code
could look like this:

```plaintext
Look! We rolled a 4
Look! We rolled a 2
Look! We rolled a 1
Look! We rolled a 1
```
