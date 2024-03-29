# APCSA

## Chapter 2 - Project 1

```
Write a program that produces the following output using nested for loops:

****** //////////// ******
*****  //////////\\  *****
****   ////////\\\\   ****
***    //////\\\\\\    ***
**     ////\\\\\\\\     **
*      //\\\\\\\\\\      *
       \\\\\\\\\\\\
```

### Step 1 - Break down what we are looking at:

| line # | stars | spaces | slash | backslash | spaces | stars |
|--------|-------|--------|-------|-----------|--------|-------|
| 1      | 6     | 1      |  12   | 0         | 1      | 6     |
| 2      | 5     | 2      |  10   | 2         | 2      | 5     |
| 3      | 4     | 3      |  8    | 4         | 3      | 4     |
| 4      | 3     | 4      |  6    | 6         | 4      | 3     |
| 5      | 2     | 5      |  4    | 8         | 5      | 2     |
| 6      | 1     | 6      |  2    | 10        | 6      | 1     |
| 7      | 0     | 7      |  0    | 12        | 7      | 0     |

We have 4 viable options keeping track of the current line in a for loop that will run 7 times
* count from 0 to 6: 0,1,2,3,4,5,6
* count from 1 to 7: 1,2,3,4,5,6,7
* count from 7 down to 1: 7,6,5,4,3,2,1
* count from 6 down to 0: 6,5,4,3,2,1,0

Do some quick calculations to see how you might line up the the current line number with the table above. Keep in mind that we are not printing the line number.

Looking at spaces and stars, it looks like they always add up to 7 characters divided between spaces and stars. We could use either the number of stars or spaces to control our loop. 

* If we choose stars we go from 6 down to 0.
* If we choose spaces we go from 1 to 7 

With spaces and stars neither of these have an advantage. So lets look at the next column, slash. Slash goes from 12 down to 0. When comparing that with the two options he currnently have, it might stand out that `6*2 = 12`, `5*2 = 10` ... `0*2 = 0`. That looks to be a better fit than using 1 to 7. So, let's get started

### Step 2 - lay out some basic plans

First make a class to hold your program and add some comments for your basic plan.

```java
public class ProjectOne {
   public static void main( String[] args ){
      // print the line
         // print the beginning stars
         // print the beginning spaces
         // print the slashes
         // print the backslashes
         // print the ending spaces
         // print the ending stars
   }
}
```

### Step 3 - Start at the first step. Printing the lines

```java
public class ProjectOne {
   public static void main( String[] args ){
      // print the line
      for( int i = 6; i >= 0; i-- ) {
         System.out.print( "line: " + i ); // we will remove this later, it helps keep track of where we are for debugging
         // print the beginning stars
         // print the beginning spaces
         // print the slashes
         // print the backslashes
         // print the ending spaces
         // print the ending stars
         
         System.out.println();
      }
   }
}
```

If you run this you will get the following output:

```
line: 6
line: 5
line: 4
line: 3
line: 2
line: 1
line: 0
```

Looks good!

### Step 4 - Identify Constants

Already, we have added a [magic number](https://en.wikipedia.org/wiki/Magic_number_(programming)). Remove that now by pulling out the 6 into a constant.

```java
public class ProjectOne {
   public static int MAX_LINE_INDEX = 6;
   public static void main( String[] args ){
      // print the line
      for( int i = MAX_LINE_INDEX; i >= 0; i-- ) {
         System.out.print( "line: " + i ); // we will remove this later, it helps keep track of where we are for debugging
         // print the beginning stars
         // print the beginning spaces
         // print the slashes
         // print the backslashes
         // print the ending spaces
         // print the ending stars
         
         System.out.println();
      }
   }
}
```

Bonus step: make sure this still works after your code change. And, of course, if you have working code, it is a good time to commit in github.

### Step 5 - Print the beginning stars

Add a for loop for the number of stars to print. Remember the combined number of stars and spaces is 7.

Using code fragments here to save some space.

```java
      // print the line
      for( int i = MAX_LINE_INDEX; i >= 0; i-- ) {
         System.out.print( "line: " + i ); // we will remove this later, it helps keep track of where we are for debugging
         
         // print the beginning stars
         for( int j = i; j > 0; j-- ){
            System.out.print( "*" );
         }
         
         // print the beginning spaces
         
         // print the slashes
         // print the backslashes
         // print the ending spaces
         // print the ending stars
         
         System.out.println();
      }
```

This will produce the output 
```
line: 6******
line: 5*****
line: 4****
line: 3***
line: 2**
line: 1*
line: 0
```

Remember the line number part is extra, we will remove that later. Also, it is worth noting that the i and j variable names don't help much here. You do need to be able to work with them since it looks like a lot of the test content uses i and j. If you want something more descriptive in your own programs, you can use better names.

### Step 6 - Print the beginning spaces

Go back and look at the table we are looking for the spaces to have a pattern

| line | i | spaces |
|------|---|--------|
| 1    | 6 | 1      |
| 2    | 5 | 2      |
| 3    | 4 | 3      |
| 4    | 3 | 4      |
| 5    | 2 | 5      |
| 6    | 1 | 6      |
| 7    | 0 | 7      |

The relationship between i (current line counter) and the number of spaces is `7 - i`

```java
         // print the beginning stars
         for( int j = i; j > 0; j-- ){
            System.out.print( "*" );
         }
         
         // print the beginning spaces
         for( int j = 0; j < (7-i); j++ ){
            System.out.print( "-" );
         }
         
         // print the slashes
```

It is hard to see spaces in our output, notice that we put in "-" temporarily to see them.

The output for this looks like: 

```
line: 6******-
line: 5*****--
line: 4****---
line: 3***----
line: 2**-----
line: 1*------
line: 0-------
```

### Step 7 - pull out the magic numbers

We introduced a new number to represent how many total characters were in the stars and spaces combined. Pull that value into a constant

```java
   public static int MAX_LINE_INDEX = 6;
   public static int SPACES_STARS_LENGTH = 7;
   public static void main( String[] args ){
```

```java
         // print the beginning spaces
         for( int j = 0; j < (SPACES_STARS_LENGTH - i); j++ ){
            System.out.print( "-" );
         }
```

### Step 8 - print the slashes

Lets look at the table again to see the relationship of slashes to our current line counter

| line | i | slashes |
|------|---|---------|
| 1    | 6 | 12      |
| 2    | 5 | 10      |
| 3    | 4 | 8       |
| 4    | 3 | 6       |
| 5    | 2 | 4       |
| 6    | 1 | 2       |
| 7    | 0 | 0       |

From the table we can see that the number of slashes is equal to `i * 2`.

Let's implement that in a for loop.

```java
         // print the slashes
         for( int j = 0; j < (i*2); j++ ){
            System.out.print("/");
         }
```

The output will look like: 
```
line: 6******-////////////
line: 5*****--//////////
line: 4****---////////
line: 3***----//////
line: 2**-----////
line: 1*------//
line: 0-------
```

Here the 2 could be pulled out into a constant as well. Seems like a good excercise for the reader at this point. Enjoy!

### Step 9 - printing the backslashes

| line | i | slashes | backslashes |
|------|---|---------|-------------|
| 1    | 6 | 12      | 0 |
| 2    | 5 | 10      | 2 |
| 3    | 4 | 8       | 4 |
| 4    | 3 | 6       | 6 |
| 5    | 2 | 4       | 8 |
| 6    | 1 | 2       | 10 |
| 7    | 0 | 0       | 12 |

Think of the same approach we too for combining stars and spaces. In this case the count slashes + backslashes is always 12. Since we know the number of slashes is `(i*2)`, we can determine that the number of backslashes is `12 - (i*2)`.

In a for loop, this looks like: 

```java
         // print the backslashes
         for( int j = 0; j < 12 - (i*2); j++ ){
            System.out.print("\\");
         } 
```

When we test this we get:

```
line: 6******-////////////
line: 5*****--//////////\\
line: 4****---////////\\\\
line: 3***----//////\\\\\\
line: 2**-----////\\\\\\\\
line: 1*------//\\\\\\\\\\
line: 0-------\\\\\\\\\\\\
```

Now that we have the right output, we need to address the magic number we introduced. In this case, we need to extract 12 into a named constant in order to express its meaning.

```java
   public static int SLASH_BACKSLASH_LENGTH = 12;
   
   for( int j = 0; j < SLASH_BACKSLASH_LENGTH - (i*2); j++ ){
```

### Step 10 - wrapping it up

We have covered the concept that duplication in your code is bad. You should put repeated code into functions that you can reuse. Here we see that we are printing the exact same number of spaces and stars as before. However, in this class, we have not covered how to pass information to those functions. Here we would need to pass down our value of i to a function that printed either the stars or the spaces. So you get a free pass to copy and paste the code to print the spaces and the code to print the stars. Enjoy this while it lasts.

```java
         // print the ending spaces
         for( int j = 0; j < (SPACES_STARS_LENGTH - i); j++ ){
            System.out.print( "-" );
         }
                  
         // print the ending stars
         for( int j = i; j > 0; j-- ){
            System.out.print( "*" );
         }
 ```
 
 Results of testing:
 
 ```
line: 6******-////////////-******
line: 5*****--//////////\\--*****
line: 4****---////////\\\\---****
line: 3***----//////\\\\\\----***
line: 2**-----////\\\\\\\\-----**
line: 1*------//\\\\\\\\\\------*
line: 0-------\\\\\\\\\\\\-------
 ```

This is looking pretty good!

### Step 11 - clean up

We added some stuff to the output to make it easier for us to see what was going on. But, those extras were not supposed to be part of our output. Now we need to clean up:

* the line counter
* the - character that was used in place of the space

Make sure in the end, you output looks like: 

```
****** //////////// ******
*****  //////////\\  *****
****   ////////\\\\   ****
***    //////\\\\\\    ***
**     ////\\\\\\\\     **
*      //\\\\\\\\\\      *
       \\\\\\\\\\\\       
```



