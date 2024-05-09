UCSD CSE15L Spring 2024 - Week 6
# Lab Report 3
---
## Part 1: Bugs

For this portion of the lab report, I chose to focus on the the bug present in the `reverseInPlace` method in the `ArrayExamples` class.
Here is the code for the `reverseInPlace` method: 
```
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

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
