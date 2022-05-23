# CSE15L Lab Report 4

For this lab report, we are looking at how my `MarkdownParse.java` and the group that we review's parser works on three complicated markdown tests.

These are the three tests we were given:

Test 1:
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```
Test 2:
```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```
Test 3:
```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```
We decided that the expected result for test 1 was ``[`google.com, google.com, ucsd.edu]``, for test 2 it was `[a.com, a.com(()), example.com]`, and for test 3 it was `[https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]`.

[Here](https://github.com/jexu07/markdown-parser) is a link to my markdown-parse repository, and [here](https://github.com/Barakar13/markdown-parser) is the markdown-parse we reviewed.

To add the tests to my parser, I used the following code:
![adding tests](lab-report-4-resources\adding-tests.png)

When I ran these tests on my parser, all three of them failed and produced the following output:
![my parser testing](lab-report-4-resources\my-parser-failures.png)

Then, I ran the tests using the other group's parser. All three of them failed as well and produced the following output:
![other group parser testing](lab-report-4-resources\other-group-parser-failures.png)

For the first test, I don't think that a small code change could fix the problem for backticks and all related cases. You can't just ignore all text between two backticks, since that would solve the first line of the test but mess up the second line. The problem is that backticks result in text not counting, but only sometimes. You would have to account for case of where backticks can occur and decide what should happen every time. A backtick can start before the open bracket and end after the open bracket, after the open parenthesis, or after the close parenthesis. Other cases like two backticks being between the open and closed brackets means the link should be counted. In addition, double backticks function identically to single backticks, so this adds complexity since counting backticks includes having to check if the next character is also a backtick.

For the second test, I also don't think a small code change could fix the problem for test 2 and all related cases about nested parentheses, brackets, and escaped brackets. This would require one while loop for the nested parentheses and another while loop for the nested brackets. The loop would have deal with there being more open brackets than closed brackets and vice versa as well as having to check for spaces that indicate the link is invalid. Checking for escaped brackets is relatively easy since you can just check if the character before the bracket is a backslash. 