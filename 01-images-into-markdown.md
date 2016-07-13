# Macro Practice: Formatting Local Images Into Markdown

## Preface
Hello, someone posted a question about practicing macros the other day.
I thought I'd start chronicling ways I use macros in my day-to-day work.
I'll explain the situation I was using them in and provide entry-level
explanations for all the commands I use. Hopefully someone learns something
from these explanations, and hopefully many people tell me ways this can
be improved. Let's all learn more tips and tricks.

## Summary
I'm editing a markdown file of lesson notes teaching beginner programmers
recursion. A coworker made some awesome diagrams showing the call stack during
recursive calls. I want to add those diagrams to this document.

Ok, I remember the markdown syntax for includes images, which is like
`![image description](file.png)`.

## Inserting File Names

Hmm. Wait, what were all those files called again?
I hate remembering and transcribing things like file names.
It's too easy to make a small mistake and get something wrong.

I know I already put the images in the current directory. Let's have vim
read the result of a bash `ls` command to get the names of all the files
in the current directory and write them into this file.

```bash
:r !ls
```

Here's a breakdown of what's going on there:

```txt
ESC   # always press escape to get outta insert mode
:     # press colon to enter a command
r !   # the r command in normal mode reads input from
ls    # a common bash command that prints a list of files in the current directory.
```

Now the file is filled with text listing all the files in my current directory.
I'll use this text as "dough" to knead and bake into delicious "bread text" that
I really want.

```txt
call-stack-fibonacci.png
call-stack-palindrome.png
call-stack-reverse.png
readme.md
recursion_droste.jpg
recursion_hulk_hogan.jpg
recursion_mona_lisa.jpg
```

I visually select the last lines after the PNGs I want. (Yes, I know I could have
used a better `ls *.png` to reduce the list. Perhaps I'll do that next time. Let's
say for the sake of argument I didn't remember what format the files were saved as.)

Now I've deleted the other lines of files and I've just got this.

```txt
call-stack-fibonacci.png
call-stack-palindrome.png
call-stack-reverse.png
```

## Recording the Macro

Woohoo! This is a prime candidate for using macros!

I always like to record my macros following this pattern:

```txt
ESC   # always escape from insert mode
qa    # begin recoding into register a
0     # press zero to go to the beginning of the line
i     # enter insert mode
...   # here is where the actual custom content goes
j     # move to the next line so I can rerun this quickly
q     # stop recording
```

Here's my full macro for this edit:

```
ESC   # always escape from insert mode
qa    # begin recoding into register a
0     # press zero to go to the beginning of the line
i     # enter insert mode
![](  # insert the first text I want
ESC   # leave insert mode
A     # append to the end of the line
ESC   # leave insert mode
j     # move to the next line so I can rerun this quickly
q     # stop recording
@a    # play the macro that was savedd to a
@@    # play the last macro again
```

And after that now my file looks like this! I can move back through the
backets and enter in descriptions for each image if I want.

```txt
![](call-stack-fibonacci.png)
![](call-stack-palindrome.png)
![](call-stack-reverse.png)
```

And with that macros saved me a tiny amount of work and I had some fun along the way.

It's way easier for me to reason about one-off macros like this than it is
for me to reason about how to do this same thing with regular expressions. :)
