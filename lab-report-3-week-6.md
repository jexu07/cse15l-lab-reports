# CSE15L Lab Report 3

This report goes over implementing the three group choice options that we were given during lab 5. 

## Part 1: Streamlining ssh Congifuration

Unfortunately, I was unable to get this part to work. I edited the config file using notepad and typed out all the information.

![config.txt not working](lab-report-3-resources\config-does-not-work.png)

I have the HostName as the target host, the User as my account name, and the IdentityFile as my private rsa key. However, when I typed `ssh ieng6` into the command line, it did not work and instead prompted me for a password.

![password lol](lab-report-3-resources\ssh-failure-password.png)

When I typed in my account password, it did not work and I exited using Ctrl + c. I tried searching online which suggested things like using `chmod`, but it did not work and I was unable to figure it out.


## Part 2: Setup Github Access from ieng6

This part involved setting up ssh keys for Github.