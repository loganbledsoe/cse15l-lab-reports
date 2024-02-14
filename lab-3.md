# Lab Report 3

## Part 1 - Bugs

**Method:** `averageWithoutLowest(double[] arr)`

**Inputs**

The failure producing and non-failure producing inputs are included in the `testAverageWithoutLowest()` test below.
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

**Symptom**

![Screenshot of junit tests running](lab-report-3-img-1.png)

| **Type**                 | **Input**                   | **Expected** | **Actual** |
|----------------------|-------------------------|----------|--------|
| Non-Failure Inducing | 4.0, 3.5, 1.1, 2.2, 4.0 | 3.4250   | 3.4250 |
| Failure Inducing     | 3.4, 2.0, 5.0, 2.0      | 3.4667   | 2.8000 |

**Bug**

Before:
```java
static double averageWithoutLowest(double[] arr) {
        if (arr.length < 2) {
            return 0.0;
        }
        double lowest = arr[0];
        for (double num : arr) {
            if (num < lowest) {
                lowest = num;
            }
        }
        double sum = 0;
        for (double num : arr) {
            if (num != lowest) {
                sum += num;
            }
        }
        return sum / (arr.length - 1);
    }
```

After:
```java
static double averageWithoutLowest(double[] arr) {
        if (arr.length < 2) {
            return 0.0;
        }
        double lowest = arr[0];
        for (double num : arr) {
            if (num < lowest) {
                lowest = num;
            }
        }
        double sum = 0;
        for (double num : arr) {
            sum += num;
        }
        sum -= lowest;
        return sum / (arr.length - 1);
    }
```

The issue with the method was that, when summing over the array, it would not inclue any numbers that were equal to the lowest, rather than just the lowest.
The updated method above instead sums the *entire* array then subracts the lowest from that sum.

## Part 2 - Researching Commands
**Command:** `find`

**Option 1:** `-mtime`
```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -mtime -1
plos/
plos/empty-directory
plos/empty.txt
plos/paradox.txt
```
The `-size` option filters the result of the `find` command to
any files or directories modifided either between some time and now or before some time (specified by a number of days in the past).
(`-` for between some time and now and `+` for before some time)
In this example, the the command finds all files/directories in `plos/` modified in the last day.
This could be useful as it allows you to see any recent changes.

```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find biomed/ -mtime -5
 
```
Now, the command tries to find all files/directories in `biomed/` modified within the last `5` days.
There are none, so is output is empty.
This is useful for verifying there are no recently modified files in a directory.

**Option 2:** `-empty`
```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -empty
plos/empty-directory
plos/empty.txt
```
The `-empty` option filters the result of the `find` command to
any files or directories that are empty.
In this example, the the command finds one empty text file and one empty directory within `plos/`.
This might be useful for finding files/directories that are useless and should be deleted.

```

Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find biomed/ -empty
 
```
Now, the command tries to find empty files/directories in `biomed/` but finds none.
So, its output is empty. This is useful for a similar reason as the last example,
but in this case shows there are no such files.

**Option 3:** `-size`
```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -size +35k
plos/pmed.0010028.txt
plos/pmed.0010036.txt
plos/pmed.0020018.txt
plos/pmed.0020059.txt
plos/pmed.0020073.txt
plos/pmed.0020103.txt
plos/pmed.0020182.txt
plos/pmed.0020246.txt
plos/pmed.0020249.txt
```
The `-size` option filters the result of the `find` command to
any files or directories small or larger in size than the given number. (`-` for smaller than and `+` for greater than) (k for kilobytes, M for megabytes)
In this example, the command finds the few files in `plos/` greater than `35kB`.
This would be useful to see which files are taking up a lot of space.
You might then do something with these files such as delete them.

```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -size -2k
plos/
plos/empty-directory
plos/empty.txt
plos/paradox.txt
plos/pmed.0020191.txt
plos/pmed.0020226.txt
```
Now, the command finds the files/directories in `plos/` less than `2kB`.
This would be useful to see which files are not taking up lots of space.

**Option 4:** `-delete`

```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ ls
911report/  biomed/  government/  plos/

Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find biomed/ -delete
 
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ ls
911report/  government/  plos/
```
The `-delete` option, when added to the end of a `find` command deletes any files or folders that would have otherwise just been printed by the command.
In this example, it deletes the entire directory `biomed/`, behaving similarly to `rm -r biomed/`.

```
Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -empty
plos/empty-directory
plos/empty.txt

Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -empty -delete

Logan@DESKTOP-46LB60O MINGW64 ~/OneDrive/Desktop/lab-5/docsearch/technical (main)
$ find plos/ -empty
 
```
Now, using both the `-empty` and `-delete` options, the command deletes all *empty* files in `plos/`.
This is a way in which you might clean up unnecessary (though not always) files/folders

**Sources**
For all options above, the sources are as follows:
- ChatGPT with the prompt "What are some useful options/flags for the find command in bash?" This provided a starting point of options to further research with the man command and --help option. (No text in this report was written by AI.)
- The man command and --help option.
