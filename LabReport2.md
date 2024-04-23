UCSD CSE15L Spring 2024 - Week 4
# Lab Report 2 
---
## Part 1: `ChatServer`
The screenshot below shows the code for my `ChatServer`.
![Image](Lab2Photo1.png)

Running the first `/add-message` command:
![Image](Lab2Photo2.png)
After running `curl "http://localhost:4000/add-message?s=Welcome%20to%20Lecture&user=Professor"`:
* The method `handleRequest(URI url)` from the `Handler` class is called after making the first `curl` request.
* Argument is a `URI` passed by the `curl` command: `/add-message?s=Welcome%20to%20Lecture&user=Professor`
* Relevant field of the `Handler` class is the string `chatLog`, which is an empty string before the request
* This specific request changes the value of `chatLog` from `“”` to `“Professor: Welcome to Lecture \n;”`

Running the second `/add-message` command:
![Image](Lab2Photo3.png)
After running `curl "http://localhost:4000/add-message?s=Come%20to%20Office%20Hours%20for%20help&user=TA"`:
* The method `handleRequest(URI url)` from the `Handler` class is called again after making the second `curl` request.
* Argument is a `URI` passed by the `curl` command: `/add-message?s=Come%20to%20Office%20Hours%20for%20help&user=TA`
* Relevant field of the `Handler` class is the string `chatLog`, which is `“Professor: Welcome to Lecture \n;”` before the request.
* This specific request changes the value of `chatLog` from `“Professor: Welcome to Lecture \n;”` to `"Professor: Welcome to Lecture\nTA: Come to Office Hours for help\n"` 

---
## Part 2: `SSH`
![Image](Lab2Photo4.png)
![Image](Lab2Photo5.png)
![Image](Lab2Photo6.png)
---
## Part 3: What I Learned
---
