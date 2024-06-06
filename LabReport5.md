UCSD CSE15L Spring 2024 - Week 10
# Lab Report 5 - Putting it All Together 
---
## Part 1 - Debugging Scenario

This portion of the lab report is written as a conversation on Piazza containing:

1) The original post from a student with a terminal output showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is.

Title: Issue with Running grade.sh Script - Incorrect Test Results

Body: 
Hello, I am having trouble running the `grade.sh` script. It fails some tests in `TestListExamples.java`; here is the content of my `grade.sh` script: 
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir student-submission
mkdir grading-area

# Step 1: clone the students repo
git clone $1 student-submission
echo 'Finished cloning'

# Step 2: check student code contains ListExamples.java
if [[ -f student-submission/ListExamples.java ]]; then 
    echo "ListExamples.java Exists"
else
    echo "ListExamples.java does not exist"
    echo "Grade: 0"
    exit 
fi 

# Step 3: Put all the relevant files in the grading-area directory. 
# ListExamples.java, TestListExamples.java, lib directory
cp TestListExamples.java grading-area/  # Ensure this is the correct reference
cp student-submission/ListExamples.java grading-area/
cp -r lib grading-area/


#Step 4: Compile the java files and check that they compiled successfully
cd grading-area
javac -cp $CPATH ListExamples.java TestListExamples.java

echo "The exit code of java is $?"

if [[ $? -ne 0 ]]; then
    echo "Failed to compile"
    exit 1
else
    echo "Compiled successfully"
fi


#Step 5: Run the tests and report the grade based on the JUnit output

# Capture output of JUnit
junit_result=$(java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples)
echo "JUnit Output:"
echo "$junit_result"

# Assuming junit_result contains the output from JUnit
total_tests=$(echo "$junit_result" | grep -o "OK ([0-9]* tests)" | grep -o "[0-9]*")
failures=$(echo "$junit_result" | grep -o "Failures: [0-9]*" | awk '{print $2}')
total_tests=${total_tests:-0}
failures=${failures:-0}

# echo "Total tests parsed: $total_tests"
# echo "Failures parsed: $failures"

if [ "$total_tests" -gt 0 ]; then
    successful_tests=$((total_tests - failures))
    success_rate=$((100 * successful_tests / total_tests))
    echo "Grade: $success_rate%"
else
    echo "Grade: 0%"
fi
```
I get the following output when I call the script with the following command: `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected.git`

Output:
```
Finished cloning
ListExamples.java Exists
Compiled successfully
JUnit Output:
JUnit version 4.13.2
.E.
Time: 0.007
There was 1 failure:
1) testFilter_allMatch(TestListExamples)
java.lang.AssertionError: expected:<[apple, apricot, banana]> but was:<[]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at TestListExamples.testFilter_allMatch(TestListExamples.java:20)

FAILURES!!!
Tests run: 3,  Failures: 1
Grade: 66%
```
2) A response from a TA asking a leading question or suggesting a command to try.
Response: There may been an issue with the implementation of the filter method in `ListExamples.java`. Can you print out the filtered list inside the filter method to check what elements are being added?

3) Another terminal output showing what information the student got from trying that, and a clear description of what the bug is.
Here is the new output:
```
Filtered List: []
java.lang.AssertionError: expected:<[apple, apricot, banana]> but was:<[]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at TestListExamples.testFilter_allMatch(TestListExamples.java:20)
```
Since filtered list is empty, the `StringChecker` might not be working as expected. 

5) At the end, all the information needed about the setup including:
- The file & directory structure needed:
```
-  GradeServer.java
-  ListExamples.java
-  Server.java
-  TestListExamples.java
-  grade.sh
-  lib
    - hamcrest-core-1.3.jar
    - junit-4.13.2.jar
```
- The contents of each file: https://github.com/jjsyucsd/grader-review-jjsy
- The full command line (or lines) you ran to trigger the bug
- `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected.git`
- A description of what was edited to fix the bug: In `TestListExamples.java`, changed `return s.startsWith(validPattern);` to `return s.contains(validPattern);`

---
## Part 2 - Reflection
In the second half of this quarter, I started using Vim and found it to be a really powerful text editor. It has the potential to be more efficient by using the keyboard instead of a mouse. I'm still starting the learning curve, but I'm planning to learn more shortcuts that will allow for faster traversal through code. I plan to keep using Vim in my future classes to develop the habit and be less dependent on the mouse. This experience has shown me that with the right system, I can streamline productivity, and I'm looking forward to seeing how long it will take to master Vim.


