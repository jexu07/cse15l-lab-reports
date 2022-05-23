# CSE15L Lab Report 4

For this lab report, we are looking at how my `MarkdownParse.java` and the group that we reviewed's parser works on three complicated markdown tests.

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

For the second test, I also don't think a small code change could fix the problem for test 2 and all related cases about nested parentheses, brackets, and escaped brackets. This would require one while loop for the nested parentheses and another while loop for the nested brackets. The loop would have deal with there being more open brackets than closed brackets and vice versa as well as having to check for spaces that indicate the link is invalid. Checking for escaped brackets is relatively easy since you can just check if the character before the bracket is a backslash. While a doable fix, it is more complex than a small code change.

For the third test, I also don't think a small code change could fix the problem for test 3 and all related cases regarding newlines in brackets and parentheses. I think fixing parentheses will be easy, since spaces already prevent something from being a link and newlines are represented as spaces. So, checking for spaces in the link will also check for newlines. However, fixing newlines in brackets is more difficult since you can put as many spaces between words as you want, so checking for spaces won't work here. I don't know how what else I could do to fix this. I would have to look into exactly how newlines are represented in markdown that makes them unique from spaces. If I could figure out a way to check for newlines, then fixing this would be simple since I could ignore links which have two or more consecutive newlines in the text between the brackets.

This lab was a good lesson in making sure that your code works in edge cases. Although I thought my markdown parser was fairly solid, these examples exposed that there were cases I hadn't thought of that my parser failed on. I have gained more respect for people who create tools like Markdown, since they have to account for every case that could possibly happen, even if they are rare occurances.