# Lab Report 5 - Week 9
## Part 1 - Debugging Scenario

### Original Post
Hi! I've written a method to sort an array of integers using the bubble sort algorithm.
It passes all my tests except one, and I cannot figure out why. The input is `{ 5, 8, 1, 2, 3, 4, 5, 6 }`, so I expect the array to be sorted into `{ 1, 2, 3, 4, 5, 5, 6, 8 }`.
But instead it becomes `{ 1, 1, 2, 3, 4, 5, 5, 6 }`. Every element is in the correct order, but some are missing, and some are duplicated.
I've looked though my code a bunch of times and I can't seem to find anything that would cause this.

![test results](resources/lab-9/test-results.png)

### TA Response

### What the Sutdent Got From the Response

### Setup Information

**File & Directory Structure**
```
|- Project/
    |- lib/
        |- hamcrest-core-1.3.jar
        |- junit-4.13.2.jar
    |- Sort.java
    |- SortTests.java
    |- test.sh
```

**Sort.java**
```java
class Sort {
    static void BubbleSort(int[] arr) {
        int temp;
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                temp = arr[i];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                }
            }
        }
    }
}
```

**SortTests.java**
```java
import org.junit.Test;

import static org.junit.Assert.*;

public class SortTests {
    @Test
    public void testBubbleSortSortedAlready() {
        int[] input = { 1, 2, 3, 4, 5 };
        int[] expected = { 1, 2, 3, 4, 5 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen1() {
        int[] input = { 10 };
        int[] expected = { 10 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen3() {
        int[] input = { 2, 1, 3 };
        int[] expected = { 1, 2, 3 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen8() {
        int[] input = { 5, 8, 1, 2, 3, 4, 5, 6 };
        int[] expected = { 1, 2, 3, 4, 5, 5, 6, 8 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }
}
```

**test.sh**
```sh
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore sortTests
```