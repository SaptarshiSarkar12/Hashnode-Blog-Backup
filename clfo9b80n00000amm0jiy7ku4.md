---
title: "Debugging : My Experience"
seoTitle: "Debugging: My Experience and Recommendations"
seoDescription: "Here is my experience of the troublesome task of debugging code, finding issues, solving them and my recommendations."
datePublished: Sat Mar 25 2023 17:40:09 GMT+0000 (Coordinated Universal Time)
cuid: clfo9b80n00000amm0jiy7ku4
slug: debugging-my-experience
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/m_HRfLhgABo/upload/efc282e50e2acfe4dd1900b42c467598.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1679766210904/60d34b8d-e772-4081-ad19-4f29731c167c.webp
tags: java, debugging, javafx, experience, wemakedevs

---

This week I was working on an **open-source project** - [Drifty](https://github.com/SaptarshiSarkar12/Drifty) which is a File Downloader System built using **Java**. I was assigned to [create a **GUI** (*Graphical User Interface*)](https://github.com/SaptarshiSarkar12/Drifty/pull/203) version for [Drifty](https://github.com/SaptarshiSarkar12/Drifty).

# Starting with the project

I created a [Maven](https://maven.apache.org/) project in [IntelliJ Idea](https://www.jetbrains.com/idea/) IDE. The project (*Drifty*) **did** not have separate packages for **Backend** and **CLI** (*Command Line Interface).* The CLI was integrated with the **Backend**, so, adding a **GUI** would be a *difficult* task to do. Moreover, the GUI code can not be maintained well. So, I spent a great deal of time separating the **Backend** from the **CLI**. Finally, I was done. The process went well.

I created a separate package for the GUI version, installed all the dependencies and started the next process. I wrote some code to show a window with the required title, window size, etc. and ran the code. Hooray🥳! The code worked! 🎉

I wrote some more lines of code to make the whole GUI application functional with the Backend which deals with downloading the file.

# Bug enters...

I created `TextFields` and `TextArea` in the GUI app, that takes inputs from the user and displays outputs. I created a `Progress Bar` to show the progress of the file download. Everything was alright but when I ran the code, it failed❗

```bash
Prism ES2 Error - nInitialize: glXChooseFBConfig failed
```

A **runtime error** has occurred. I got surprised when I **could not** find the solution to this error **ANYWHERE**❗

An idea struck my mind 💡!

*IntelliJ* has an option to **Invalidate Cache and Restart**. I clicked on that. The IDE restarted and *fortunately*, the **Error** has **GONE**! I excitedly ran the code again - The Build process went smoothly, but, after waiting for *more than 5 minutes*, the GUI **window** *did* ***NOT*** *show up*❗I searched about the problem but **did not find** a solution to this exact problem.

# What I did

As multiple threads were running when the program started, so, a `printStackTrace()` method would always lead me to the `Thread` class as the root of the error.

The `start()` method is the main method for a *JavaFX application*, which is called from the `main()` method when the application launches. So, I ***commented*** *out method calls* from **down to the top**, *leaving the* ***first method*** ***call*** which initializes the window. I ran the program again, but, the window still did not appear 😰.

Now, I straight away went into the method and repeated the above process. I ran the code once more, and fortunately, the window successfully appeared.

After carefully examining the method calls that I have made, I found the method `mainWindow.sizeToScene()` was causing the problem. This method caused *the window size to* ***overflow*** *from the screen,* hence the **window did not turn up**. I quickly uncommented the whole program code and removed this (`mainWindow.sizeToScene()`) method call. The program was successfully executed ✅ and the window appeared 😅 !

Here is a [link to the commit](https://github.com/SaptarshiSarkar12/Drifty/pull/203/commits/af82c661fd6a29205e6e5f34e375ead1a9da456e#diff-18045516e3c555eb9197f8f12bf56f0ebd8386c15d6f0fa39e4fd4fa105143b3) that I made to solve the issue.

# Conclusion

I have tried out a *new way* to **debug code** without using ***standard debuggers*** that come packaged with *IDEs*. This helped me to find bugs in my code and fix them, when *the debuggers* packaged with IDEs, **point to the wrong cause** of the problem.

Here is what I learned and some of my recommendations -

* Examine and understand from what point the actual application starts.
    
* Comment out or remove method calls from the bottom part of the program to the top, leaving the main method call uncommented.
    
* Run the code.
    
* Check if the error occurs.
    
* If yes, go inside the uncommented method and comment out all the lines leaving the main topmost lines crucial for the application to start.
    
* Run and check for the error.
    
* If the error still exists, repeat the process.
    
* After some time, it will get fixed ultimately.
    

You may use websites like [**Stack Overflow**](https://stackoverflow.com/) to fix the problem with greater velocity.

---

Hello 👋, I'm **Saptarshi Sarkar**, a ***Software Developer*** and ***an open-source enthusiast***.

Thank you for reading the article!

Feedback to improve this blog is appreciated and warmly welcomed. If you liked my blog, do *share it*.

### Connect with me -

🔗 [All my links](https://bio.link/saptarshi) | [Twitter](https://twitter.com/SSarkar2007) | [GitHub](http://github.com/SaptarshiSarkar12/) | [LinkedIn](https://www.linkedin.com/in/saptarshi-sarkar-305162253/)