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
