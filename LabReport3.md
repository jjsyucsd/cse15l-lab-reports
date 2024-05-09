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

* Example 1: In this example, we use `grep -r` to search all text files within `./technical` (including text files contained within subdirectories) for the string "middle-class".
```
jake@Jakes-MacBook-Pro technical % grep -r middle-class
./government/Media/Raising_the_Bar.txt:His middle-class upbringing in the '50s and '60s produced a
./government/Media/Working_for_Free.txt:button-down shirts, Zucker grew up in an upper-middle-class enclave
./government/Media/A_helping_hand.txt:the need despite having a middle-class upbringing. But a
./911report/chapter-5.txt:                middle-class family headed by his father, an attorney. After graduating from Cairo
jake@Jakes-MacBook-Pro technical %
```

* Example 2: In this example, we use `grep -r` to search all files within the `./technical` for email addresses by matching the pattern "@."
```
jake@Jakes-MacBook-Pro technical % grep -r "@.*\." .

./government/Gen_Account_Office/d0269g.txt:calboml@gao.gov,or Tom Broderick, Assistant Director,
./government/Gen_Account_Office/d0269g.txt:broderickt@gao.gov
./government/Gen_Account_Office/d0269g.txt:fraudnet@gao.gov,or
./government/Gen_Account_Office/Testimony_cg00010t.txt:"info" in the body to: Info@www.gao.gov or visit GAO's World Wide
./government/Gen_Account_Office/Testimony_cg00010t.txt:Email: fraudnet@gao.gov 18004245454 (automated answering
./government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt:yellowbook@gao.gov.To ensure that your comments are
./government/Gen_Account_Office/Sept27-2002_d02966.txt:HighlightsTest@gao.gov.
./government/Gen_Account_Office/Sept27-2002_d02966.txt:mihmj@gao.gov. Janice Lichty and BryanRasmussen were
./government/Gen_Account_Office/Sept27-2002_d02966.txt:fraudnet@gao.gov
./government/Gen_Account_Office/Sept27-2002_d02966.txt:NelliganJ@gao.gov(202) 512-4800
./government/Gen_Account_Office/d01376g.txt:can be reached at (202) 512-7957 or DiamondL@GAO.GOV. Key
./government/Gen_Account_Office/d01376g.txt:info@www.gao.gov
./government/Gen_Account_Office/d01376g.txt:• e-mail: fraudnet@gao.gov •
./government/Gen_Account_Office/pe1019.txt:info@www.gao.gov
./government/Gen_Account_Office/Testimony_Jul15-2002_d02940t.txt:Acknowledgments mihmj@gao.gov. Individuals making key
./government/Gen_Account_Office/gg96118.txt:info@www.gao.gov
./government/Gen_Account_Office/July11-2001_gg00172r.txt:send email message with "info" in the body to: info@www.gao.gov or
./government/Gen_Account_Office/July11-2001_gg00172r.txt:EMail: fraudnet@gao.gov Telephone: 18004245454 (automated
./government/Gen_Account_Office/d01121g.txt:digitalguide@gao.gov. We will assess your request and inform you of
./government/Gen_Account_Office/d01121g.txt:preceding letter, send your e-mail request to digitalguide@gao.gov.
./government/Gen_Account_Office/d03419sp.txt:SteinhoffJ@gao.gov.
./government/Gen_Account_Office/d03419sp.txt:fraudnet@gao.gov
./government/Gen_Account_Office/d03419sp.txt:NelliganJ@gao.gov(202) 512-4800
./government/Gen_Account_Office/Testimony_d01609t.txt:info@www.gao.gov
./government/Gen_Account_Office/Testimony_d01609t.txt:fraudnet@gao.gov Automated answering system: 18004245454
./government/Gen_Account_Office/d03273g.txt:E-mail: fraudnet@gao.gov
./government/Gen_Account_Office/d03273g.txt:Jeff Nelligan, managing director, NelliganJ@gao.gov (202)
./government/Gen_Account_Office/Oct15-1999_gg00026t.txt:info@www.gao.gov
./government/Gen_Account_Office/d03232sp.txt:at AgencyProtocols@gao.gov.
./government/Gen_Account_Office/d03232sp.txt:e-mail to AgencyProtocols@gao.gov.
./government/Gen_Account_Office/June30-2000_gg00135r.txt:send email message with "info" in the body to: info@www.gao.gov or
./government/Gen_Account_Office/June30-2000_gg00135r.txt:EMail: fraudnet@gao.gov Telephone: 18004245454 (automated
./government/Gen_Account_Office/d01591sp.txt:info@www.gao.gov
./government/Gen_Account_Office/d01591sp.txt:• e-mail: fraudnet@gao.gov •
./government/Gen_Account_Office/Oct15-2001_d0224.txt:mail me at daceyr@gao.gov. Major contributors to this
./government/Gen_Account_Office/Oct15-2001_d0224.txt:fraudnet@gao.gov, or1-800-424-5454 (automated
./government/Gen_Account_Office/Oct15-2001_d0224.txt:Jeff Nelligan, Managing Director, NelliganJ@gao.gov (202)
./government/Gen_Account_Office/d01145g.txt:info@www.gao.gov
./government/Gen_Account_Office/d01145g.txt:e-mail: fraudnet@gao.gov
./government/Gen_Account_Office/InternalControl_ai00021p.txt:info@www.gao.gov
./government/Gen_Account_Office/d01186g.txt:info@www.gao.gov
./government/Gen_Account_Office/d01186g.txt:• e-mail: fraudnet@gao.gov •
./government/Gen_Account_Office/ai00134.txt:to me at (202) 5122600, steinhoffj.aimd@gao.gov, or Linda Garrison,
./government/Gen_Account_Office/ai00134.txt:info@www.gao.gov
./government/Gen_Account_Office/ai00134.txt:• e-mail: fraudnet@gao.gov •
./government/Gen_Account_Office/ai9868.txt:at 202-512-6240 or brockj.aimd@gao.gov.
./government/Gen_Account_Office/May1998_ai98068.txt:at 202-512-6240 or brockj.aimd@gao.gov.
./government/Gen_Account_Office/d02701.txt:fraudnet@gao.gov
./government/Gen_Account_Office/d02701.txt:NelliganJ@gao.gov(202) 512-4800
./government/Gen_Account_Office/ai2132.txt:info@www.gao.gov
./government/Gen_Account_Office/ai2132.txt:• e-mail: fraudnet@gao.gov •
./government/Post_Rate_Comm/Mitchell_RMVancouver.txt:to rmit@iname.com.
./government/Post_Rate_Comm/Mitchell_6-17-Mit.txt:robert.w.mitchell@prc.gov or 1333 H ST NW Suite 300, Washington DC
./government/Media/highlight_Senior_Day.txt:at 522-3069 or mailto:richard.ingham@okdhs.org
./government/Media/Wingates_winds.txt:bbennett@herald.com
./government/Media/Avoids_Budget_Cut.txt:Reach Stephanie Hoops at stephanie.hoops@tuscaloosanews.com or
./government/Media/Marylands_Legal_Aid.txt:Services Corp. He can be reached at rhudy@mlsc.org. Joe Surkiewicz
./government/Media/Marylands_Legal_Aid.txt:email is jsurkiewicz@mdlab.org.
./government/Media/A_helping_hand.txt:By Joanna Corman / joanna.corman@latimes.com
./government/Media/Retirement_Has_Its_Appeal.txt:617-523-5600 or e-mail Senior Lawyers @aol.com.
./plos/pmed.0010060.txt:        Unfortunately, the availability of review documents on Drugs@FDA is sporadic. To take
./biomed/gb-2002-3-9-research0046.txt:          mged-mage@lists.sourceforge.net, which is available as a
./biomed/1471-2105-3-2.txt:        , "A Story" [ 63 ] , and "AA.AG@helix.ends" [ 64 ] ) and
./biomed/1471-2148-1-4.txt:          should be addressed to S.B.H. (e-mail: sbh1@psu.edu) or
jake@Jakes-MacBook-Pro technical %
```







