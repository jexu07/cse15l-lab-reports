# CSE15L Lab Report 3

This report goes over implementing the three group choice options that we were given during lab 5. 

## Part 1: Streamlining ssh Congifuration

Unfortunately, I was unable to get this part to work. I edited the config file using notepad and typed out all the information.

![config.txt not working](lab-report-3-resources\config-does-not-work.png)

I have the HostName as the target host, the User as my account name, and the IdentityFile as my private rsa key. However, when I typed `ssh ieng6` into the command line, it did not work and instead prompted me for a password.

![password lol](lab-report-3-resources\ssh-failure-password.png)

When I typed in my account password, it did not work and I exited using Ctrl + c. I tried searching online which suggested things like using `chmod`, but it did not work and I was unable to figure it out.


## Part 2: Setup Github access from ieng6

This part involved setting up ssh keys for Github. It also doesn't make any sense.


## Part 3: Copying whole directories with `scp -r`

I copied my markdown-parser directory to my ieng6 account.
![start copy](lab-report-3-resources\start-copy.png)
![end copy](lab-report-3-resources\end-copy.png)

There were about 30 more files that had names with random numbers and characters, and I cropped them out of the image. After copying, I logged into my course account and successfully compiled and ran the markdown parse tests.

![running ieng6 tests](lab-report-3-resources\running-test-ieng6.png)

To finish it off, I tried running everything in one line, but I got errors when trying to compile and run `MarkdownParseTest.java` on the remote server the same line. It does not give me errors when I connect the server and run the compile and run commands there.

![all-pt1](lab-report-3-resources\all-1.png)
![all-pt2](lab-report-3-resources\all-2.png)
![all-pt3](lab-report-3-resources\all-3.png)