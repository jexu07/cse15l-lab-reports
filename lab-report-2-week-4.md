# CSE15L Lab report 2:

This report deals with bugs in a program called `MarkdownParse.java` ([here](https://github.com/nidhidhamnani/markdown-parser/blob/9cc42a8f0b4f1d6eeb83bab8ba245fa8887fdd5f/MarkdownParse.java)) which is intended to look through a markdown file and return any links it has. The original file had many bugs, so we used it to practice debugging. We found failure-producing inputs and identified symptoms and bugs to improve the program.  

<br>

## Test #1:

The first test we did was on the file `testing.md` ([here](https://github.com/jexu07/markdown-parser/blob/9e89bb194e13f7e2962ecf52329de419f3c8a199/testing.md?plain=1)). The test was a failure-producing input for the first version of `MarkdownParse.java`. The symptom of this input is an infinite loop that ends up causing java to run out of memory.

![infinite loop 1](lab-report-2-resources\first-infinite-loop-error.png)

The bug that causes this infinite loop is that `currentIndex` is never updated to be greater than `markdown.length()` because there is text after the last close parenthesis. This causes the condition inside the while loop to always evaluate to true and is the bug responsible for our symptom of an infinite loop. The bug was fixed by adding a break statement so the while loop stops if a bracket or parenthesis is not found.

This is a screenshot of the code we changed to fix it.

![changedcode](lab-report-2-resources\first-code-change.png)

<br>

## Test #2:

The second test we did was on `test-file2.md` ([here](https://github.com/xicoreyes513/markdown-parser-copy/blob/a4316851b247c69e9c651aa3a8ae55d00c5817fe/test-file2.md?plain=1)). This was a failure-producing input that also went into an infinite loop and ran out of memory, but the bug and fix were different. 

![second infinite loop](lab-report-2-resources\first-infinite-loop-error.png)


Even though the first fix would have solved the memory error, it would have produced an incorrect output. This is because there are two bugs in this case. The first is that there is text after the last close parenthesis. The second one is that the link contains parenthesis, causing the program to list an incorrect link. The program that only fixes the infinite loop prints `[http://msdn.microsoft.com/en-us/library/aa752574(VS.85]` our our output, which is not the complete link in oour test file.

This is fixed for our test by checking if there is an open parenthesis in our link and updating `closeParen` if there is one. Here is a screenshot of the code we changed to make this test work.

![test 2 code change](lab-report-2-resources\second-code-change.png)


## Test #3:

This test involved the file `break-test.md` ([here](https://github.com/gabrielseventhucsd25/markdown-parser/blob/8a5ae06d9fe3b1583e25c0f7e9bdb4eabcd813d3/break-test.md?plain=1)). This was a failure-producing input because it incorrectly gathered the links. The output we got was

![third output](lab-report-2-resources\third-output.png)
but we wanted it to print `[https://en.wikipedia.org/wiki/Diego_(tortoise), about:blank]`. 

The bug is that the link includes a pair of parenthesis, so our program thinks that the link ends earlier than it does. As such, it fails to print out the correct link. 

To make the program work for this test, we added a statement to check for a newline character instead of a close parenthesis. This works for this test specifically, but is extremely likely to introduce more bugs.

![third code change](lab-report-2-resources\third-code-change.png)