
# CSE15L Lab Report 1:

This is a tutorial on how to log into your specific account on `ieng6`. I am using Windows, but there will be slight differences depending on your operating system.

## Step 1: Install Visual Studio Code

Download VS Code for your specific operating system from their website [here](https://code.visualstudio.com/download). After installing, you can open VSC and it should look similar to this:
![image](lab-report-1-images\VSC-intro-image.png)


## Step 2: Remote Connection

If you are on Windows, you need begin by [installing OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). 

Every student has a unique CSE15L account assigned to them, which can be found [here](https://sdacs.ucsd.edu/~icc/index.php). In VSC, open a new terminal (using ctrl + ` or by clicking Terminal -> New Terminal from the bar at the top) and type the command 

`$ ssh cse15lsp22aaa@ieng6.ucsd.edu`

Where "aaa" is replaced by the letters for your account.

If this is your first time connecting, you might see messages about an RSA key fingerprint. Type `yes` and press enter. Then enter the password for your class account. If everything goes smoothly, you see something similar to 

![image](lab-report-1-images\ssh-login.png)

If you see something like this, congratulations! You've successfully connected to a remote computer.

## Step 3: Testing commands

Let's get started with a few commands. The following basic commands are useful to play around with both on your device and on the server:

* `cd` - change directory
* `ls` - lists the folders and files in the current directory.
* `pwd` - prints the name of the current working directory.
* `cp <file-1> <file-2>` - copies the contents of file-1 to file-2. Will create a new file if file-2 doesn't already exists.
* `mkdir` - creates a new directory

Here is an example of me testing some commands:

![img](lab-report-1-images\testing-commands.png)


## Step 4: Moving Files with `scp`

When we want to copy files over from your device to a remote device, we can use `scp`. Create a file called `Message.java` and fill it with something that prints text, like
```
class Message{
        public static void main(String[] args) {
        System.out.println("Hello!");    
    }
}
```

We can transfer this file from our client to the remote device using the following command (replace "aaa" with your account's letters as usual):

`scp Message.java cse15lsp22aaa@ieng6.ucsd.edu:~/`

You should be promted for your password, similar to what happened with `ssh`. Type in your password. If the file was successfully transfered, you should get something like

![img](lab-report-1-images\scp-moment.png)

The file has successfully been transfered. Now, if you log into ieng6 using `ssh` and type `ls`, you should see the `Message.java` in your home directory. You can also run `javac` and `java` on it to print the message while connected to the server.

## Step 5: Setting an SSH Key

Typing our password every time we want to login using `ssh` or `scp` is inconvenient and time-consuming. A solution to this is `ssh` keys. The program `ssh-keygen` generates a private and public key. By putting the public key on the server and the private key on the client, you can log in by automatically comparing the keys instead of typing your password.

For Windows, make sure you are on the client and type

`ssh-keygen -t ed25519`

For other operating systems, just type 

`ssh-keygen`

You should be prompted to enter the file you want to save the key in. Press enter. You should then be prompted for a passphrase. Leave the passphrase empty and press enter. The whole process should look something like this:

![I can put anything i want here actually](lab-report-1-images\keygen-ex.png)

The public and private key are now stored in your `.ssh` directory. The next step is to copy the public key from your computer to the `.ssh` directory of the server. 

On the client, type

`scp \Users\<user-name>\.ssh\id_ed25519.pub cs15lsp22aaa@ieng6.ucsd.edu:~\.ssh\authorized_keys`

Now, you chould be able to use `ssh` and `scp` without needing to enter a password.

## Step 6: Optimizing Remote Running

Now, we want to improve the process of making a local edit to a file, such as `Message.java`, copying it to the server, and running it. 

Some things that can help are:

* Writing a command in quotes after `ssh` will automatically connect to the server, run the command, and exit the server.  
`ssh cs15lsp22aaa@ieng6.ucsd.edu "ls"`
* You can use multiple commands on the same line by separating them with a semicolon. For instance, you can try  
`javac Message.java; java Message`
* You can press the up-arrow on your keyboard to go through your recently used commands.

Here's an example of me copying and running `Message.java` in one line  
![dfskjlfsdlkjsdfkjlsfdjlhebjflnj](lab-report-1-images\one-line.png)


Congratulations! You've just learned the basics of connecting to and running commands on a remote server.