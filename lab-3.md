# Lab Report 3
## Part 1 - Bugs

**Method:** averageWithoutLowest(double[] arr)

**Inputs**
The failure producing and non-failure producing inputs are included in the testAverageWithoutLowest() test below.
```java
@Test
    public void testAverageWithoutLowest() {
        double[] sucessInput = { 4.0, 3.5, 1.1, 2.2, 4.0 };
        double[] failureInput = { 3.4, 2.0, 5.0, 2.0 };

        assertEquals(3.4250,
                ArrayExamples.averageWithoutLowest(sucessInput), 0.001);
        assertEquals(3.4667,
                ArrayExamples.averageWithoutLowest(failureInput), 0.001);
    }
```

**

| **Type**                 | **Input**                   | **Expected** | **Actual** |
|----------------------|-------------------------|----------|--------|
| Non-Failure Inducing | 4.0, 3.5, 1.1, 2.2, 4.0 | 3.4250   | 3.4250 |
| Failure Inducing     | 3.4, 2.0, 5.0, 2.0      | 3.4667   | 2.8000 |
