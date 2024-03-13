# Lab Report 5 - Week 9
## Part 1 - Debugging Scenario

```
|- Project/
    |- lib/
        |- hamcrest-core-1.3.jar
        |- junit-4.13.2.jar
    |- code/
        |- Sort.java
        |- SortTests.java
    |- test.sh
```

**Sort.java**
```java

```

**SortTests.java**
```java
import org.junit.Test;

import static org.junit.Assert.*;

public class SortTests {
    @Test
    public void testBubbleSortSortedAlready {
        int[] input = { 1, 2, 3, 4, 5 };
        int[] expected = { 1, 2, 3, 4, 5 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen1 {
        int[] input = { 10 };
        int[] expected = { 10 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen3 {
        int[] input = { 2, 1, 3 };
        int[] expected = { 1, 2, 3 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }

    @Test
    public void testBubbleSortLen8 {
        int[] input = { 5, 8, 1, 2, 3, 4, 5, 6 };
        int[] expected = { 1, 2, 3, 4, 5, 5, 6, 8 };
        Sort.BubbleSort(input);
        assertArrayEquals(expected, input);
    }
}
```

**test.sh**
```bash
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore sortTests
```