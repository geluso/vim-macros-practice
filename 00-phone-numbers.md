They're tricky now but in the long run you'll get better at them. The fact that you're attempting to use them know means you're aware of them and you'll only get better from here on out.

I use macros rarely, but they're extremely handy those few times I do use them. As I use them more I begin to understand when they're useful, when they're not useful -- and they become more useful the more I practice them!

Generally, my macros follows this pattern:

```txt
    qa      # start recording into the 'a' register. I like to record into a, b, c...
    0       # normalize by always start at the beginning of the line
    ...     # do all your actual manipulations
    j       # always go down to the next line so we can press @@ to replay the last macro
    q       # stop the recording
```

Then I press `@a` to play back the recording. And keep pressing `@@` to play it back many times. And sometimes I visually select a block of code and execute `:normalize @a` to play the recording across all lines in the block.

Here's one of my favorite example problems: create a macro to convert lines of 10-digit numbers to well-formatted phone numbers.

```txt
5552061122
5552220929
5557863742
```

becomes:

```txt
(509) 554-1122
(555) 222-0929
(555) 786-3742 
```

Here's how I accomplish that:

```txt
qa      # start recording into the 'a' register. I like to record into a, b, c...
0       # normalize by always start at the beginning of the line
i(      # start insert mode and get that first paren
right right right # right arrow three times
)       # get that other paren
space   # that that space
ESC     # get out of insert mode
right right right # go over three digits
i-      # insert a dash
ESC     # get out of insert mode
j       # always go down to the next line so we can press @@ to replay the last macro
q       # stop the recording
```


