UCSD CSE15L Spring 2024 - Week 1
# Lab Report 1 
---
In Week 1 lab, we covered three basic filesystem commands: 
* `cd`
* `ls`
* `cat`

## Command 1: `cd`

The command `cd` stands for change directory. It is used to change the current working directory. Using the `cd` command with no arguments takes you to your home directory. Using the command with a path to a directory as an argument will move the curent working directory into the specified directory. Using the command with a path to a file as an argument will result in an error. 

Example 1: Using the `cd` command with no arguments

In this example, we initially use the `pwd` command to determine the current working directory. The **absolute path** to the working directory **right before** the `cd` command is run is `/workspaces/lecture1`. After the `cd` command is run, we use the `pwd` command again and determine the current working directory has changed to `/home/codespace`. This is not an error, as running the `cd` command with no arguments takes us out of our personal workspace to the home directory on the GitHub server that hosts codespaces.
```
@jjsyucsd ➜ /workspaces/lecture1 (main) $ pwd 
/workspaces/lecture1 
@jjsyucsd ➜ /workspaces/lecture1 (main) $ cd
@jjsyucsd ➜ ~ $ pwd
/home/codespace
@jjsyucsd ➜ ~ $ 
```


Example 2: Using the `cd` command with a path to a directory

Continuing where we left off, we first use the `pwd` command to determine the current working directory. The **absolute path** to the working directory **right before** the `cd` command is run is `/home/codespace`. After the `cd` command is run, we use the `pwd` command again and determine the current working directory has changed to `/workspaces/lecture1`. This is not an error, as running the `cd` command with a path to a directory takes us out of the home directory and into the specified directory (in this case, back to my personal workspace).
```
@jjsyucsd ➜ ~ $ pwd
/home/codespace
@jjsyucsd ➜ ~ $ cd /workspaces/lecture1
@jjsyucsd ➜ /workspaces/lecture1 (main) $ pwd
/workspaces/lecture1
@jjsyucsd ➜ /workspaces/lecture1 (main) $ 
```

Example 3: Using the `cd` command with a path to a file

Continuing where we left off, we first use the `pwd` command to determine the current working directory. The **absolute path** to the working directory **right before** the `cd` command is run is `/workspaces/lecture1`. We then use the `ls` command (described in detail below) to find a file in the current working directory; we choose `Hello.java`. This results in an error, as `Hello.java` is not a directory. After the `cd` command is run, we use the `pwd` command again to confirm that the current working directory remains unchanged and is still `/workspaces/lecture1`. 
```
@jjsyucsd ➜ /workspaces/lecture1 (main) $ pwd
/workspaces/lecture1
@jjsyucsd ➜ /workspaces/lecture1 (main) $ ls
Hello.class  Hello.java  README  messages
@jjsyucsd ➜ /workspaces/lecture1 (main) $ cd Hello.java
bash: cd: Hello.java: Not a directory
@jjsyucsd ➜ /workspaces/lecture1 (main) $ pwd
/workspaces/lecture1
@jjsyucsd ➜ /workspaces/lecture1 (main) $ 
```

---
## Command 2: `ls`

The command `ls` stands for list. It is used to list the contents of a directory. Using the `ls` command with no arguments will list the contents in the current working directory. Using the command with a path to a directory as an argument will list the contents of the specified directory. Using the command with a path to a file as an argument will result in listing information regarding the specified file.

Example 1: Using the `ls` command with no arguments

In this example, I will use the `ls` command to list the contents of the directory `workspaces`. First we use the `pwd` command to verify that we are in the correct directory. The **absolute path** to the working directory **right before** the `ls` command is run is `/workspaces`; this tells us we are in the correct directory. After the `ls` command is run, we get the output `lecture1`. This is not an error, as running the `ls` command with no arguments will list the contents in the current working directory (which is `workspaces`). This tells us that the directory `workspaces` contains only the `lecture1` directory. 
```
@jjsyucsd ➜ /workspaces $ pwd
/workspaces
@jjsyucsd ➜ /workspaces $ ls
lecture1
```

Example 2: Using the `ls` command with a path to a directory

Continuing where we left off, we first use the `pwd` command to identify the current working directory we are in. The **absolute path** to the working directory **right before** the `ls` command is run is `/workspaces`. After the `ls` command is run, we get the output `Hello.class  Hello.java  README  messages`. This is not an error, as running the `ls` command with a path to a directory will list the contents in the specified directory (which is `lecture1` in this case). This tells us that the directory `lecture1` contains the files `Hello.class  Hello.java  README  messages`. 
```
@jjsyucsd ➜ /workspaces $ pwd
/workspaces
@jjsyucsd ➜ /workspaces $ ls lecture1
Hello.class  Hello.java  README  messages
```

Example 3: Using the `ls` command with a path to a file

Continuing where we left off, we first use the `pwd` command to identify the current working directory we are in. The **absolute path** to the working directory **right before** the `ls` command is run is still `/workspaces`. After the `ls` command is run, we get the output `lecture1/messages/en-us.txt`. This is not an error, as running the `ls` command with a path to a file will list information regarding the file (specifically the file name). This tells us that the path is valid and that file exists at the location specified. 
```
@jjsyucsd ➜ /workspaces $ pwd
/workspaces
@jjsyucsd ➜ /workspaces $ ls lecture1/messages/en-us.txt
lecture1/messages/en-us.txt
@jjsyucsd ➜ /workspaces $ 
```

---
## Command 3: `cat`

The command `cat` stands for concatenate. It is used to display the contents of files in the terminal by reading and printing file contents. Using the command with no arguments allows the user to type what text they would like to print to terminal. Using the command with a path to a directory as an argument will result in an error. Using the command with a path to a file will display the contents of the specified file in the terminal.

Example 1: Using the `cat` command with no arguments
```
# code block
To do: 
Need to complete Lab 1 Report
Before Lab next week
```

Example 2: Using the `cat` command with a path to a directory
```
# code block
To do: 
Need to complete Lab 1 Report
Before Lab next week
```

Example 3: Using the `cat` command with a path to a file
```
# code block
To do: 
Need to complete Lab 1 Report
Before Lab next week
```

---
