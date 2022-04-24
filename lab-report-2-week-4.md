# CSE15L Lab report 2:

This report deals with bugs in a program called `MarkdownParse.java` ([here](https://github.com/nidhidhamnani/markdown-parser/blob/9cc42a8f0b4f1d6eeb83bab8ba245fa8887fdd5f/MarkdownParse.java)) which is intended to look through a markdown file and return any links it has. The original file had many bugs, so we used it to practice debugging. We found failure-producing inputs and identified symptoms and bugs to improve the program.  

<br>

## Test 1:

The first test we did was on the file `testing.md` ([here](https://github.com/jexu07/markdown-parser/blob/9e89bb194e13f7e2962ecf52329de419f3c8a199/testing.md?plain=1)). The program failed to return anything as it got stuck in an infinite loop and eventually ran out of memory. This is a screenshot of the code we used to fix it.

![changedcode](lab-report-2-resources\first-code-change.png)

The test was a failure-producing input for the first version of `MarkdownParse.java`. The symptom of this input is an infinite loop that ends up causing java to run out of memory.

![infinite loop 1](lab-report-2-resources\first-infinite-loop-error.png)

The bug that causes this infinite loop is that after the first iteration of the while loop, `openBracket` is updated to -1 at the start of every loop. This causes the condition inside the while loop to always evaluate to true and is the bug responsible for our symptom of an infinite loop. The bug was fixed by adding a break statement if a bracket or parenthesis is not found.