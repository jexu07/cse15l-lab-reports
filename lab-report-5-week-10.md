# CSE15L Lab Report 

This lab report examines how two different implementations of `MarkdownParse.java` resulted in different errors when used on a set of test files. [This](https://github.com/jexu07/markdown-parser/commit/2e5b040a190e5a3c0295764d0c1207c2729ac4d2) is a github link the my version of the parser and [here](https://github.com/nidhidhamnani/markdown-parser/commit/8dd87e6914ae40a4321aac8e2483e349de40b03c) is a github link to the version provided in the lab.

To see the the test files that had differences, I logged into my ieng6 course account where i had cloned the two markdown parse repositories. In each one, i ran `bash script.sh > results.txt`, where the script ran the parser on all 652 test files and stored the results in `results.txt`. To compare the two, I typed `vimdiff markdown-parser-tests/results.txt markdown-parser/results.txt` which successfully used vimdiff to locate the differences between what the two parsers produced.

In total there were 13 tests which differed in the output, but we're only going to examine two tests here. The first test is test file 580 which can be found [here](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/580.md?plain=1). Below you can see the differences in what was printed. 

![test580diff](lab-report-5-resources\test-580-diff.png)

The file contained the text `![](/url)`, and the expected output was that no link is printed. My parser printed [] while the provided parser printed [/url]. My parser was correct in this case and the provided one made a mistake.

The bug in this case is that the provided parser doesn't recognize that this is an image instead of a link. Images have the same format as a link except there is an exclamation mark before the starting bracket. To fix this, code can be added to check if there is an exclamation point before the starting bracket and disregard the link if there is. 

The second test file which differed was test file 496 which can be found [here](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/496.md). Below, you can see the differences in what the two parsers produced.

![test 496 diff](lab-report-5-resources\test-496-diff.png)

The file contained the text `[link](foo(and(bar))`.The expected result is that no link is printed. My parser printed [foo(and(bar)] while the provided parser printed []. The provided parser was correct in this case and my parser made a mistake.

The bug in this case is that my code fails to properly deal with nested parentheses. Since there are more open parentheses than closed parentheses, the link should be disregarded, but my implementation does not do that. To fix this code, I would have to add some code to count and check for nested parentheses, most likely using a loop of some kind.