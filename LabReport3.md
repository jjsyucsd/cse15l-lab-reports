UCSD CSE15L Spring 2024 - Week 6
# Lab Report 3
---
## Part 1: Bugs

For this portion of the lab report, I chose to focus on the the bug present in the `reverseInPlace` method in the `ArrayExamples` class.

1. A failure-inducing input for the buggy program (as a JUnit test) is shown in the code block below:
```
@Test
  public void testReverseInPlace_FailureInducing() {
    int[] original = {1, 2, 3, 4};
    ArrayExamples.reverseInPlace(original);
    int[] expected = {4, 3, 2, 1};  // Expected output if the array was correctly reversed
    assertArrayEquals("The array should be reversed", expected, original);
  }
```

2. An input that doesn't induce a failure (as a JUnit test) is shown in the code block below:
```
@Test 
  public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }
```

3. The symptom, as the output of running the two tests above, is shown in the screenshot below. Note that one test passes and one test fails:
![Image](LabReport3Screenshot1.png)

4. The original unmodified buggy `reverseInPlace` method:
```
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
The fixed `reverseInPlace` method after changing the code:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```
5. Description of why the fix addresses the issue:
The fix resolves the issue in the original `reverseInPlace` method by guaranteeing that the loop only iterates through half of the array; this addresses the issue where elements are overwritten before they can be swapped to the correct position. The temporary variable `temp` allows the method to store the value of `arr[i]` before it is overwritten. These changes will address the failure-inducing input such that the test passes and the input no longer returns the incorrectly reversed array `{4, 3, 3, 4}`.

---
## Part 2: Researching Commands

For this portion of the lab report, I chose the command `grep`. I learned about the four interesting command-line options for `grep` I demonstrate below thanks to this GeeksForGeeks page: [grep command](https://www.geeksforgeeks.org/grep-command-in-unixlinux/#options-available-in-grep-command)

Option 1: `grep -i` for case insensitive search

* Example 1:

* Example 2:

Option 2: `grep -c` for displaying the count of number of matches

* Example 1:

* Example 2:

Option 3: `grep -v` to invert the pattern match

* Example 1:

* Example 2:

Option 4: `grep -r` to search recursively for a pattern in the directory

* Example 1:
```
jake@Jakes-MacBook-Pro technical % grep -r middle-class
./government/Media/Raising_the_Bar.txt:His middle-class upbringing in the '50s and '60s produced a
./government/Media/Working_for_Free.txt:button-down shirts, Zucker grew up in an upper-middle-class enclave
./government/Media/A_helping_hand.txt:the need despite having a middle-class upbringing. But a
./911report/chapter-5.txt:                middle-class family headed by his father, an attorney. After graduating from Cairo
jake@Jakes-MacBook-Pro technical %
```

* Example 2:






