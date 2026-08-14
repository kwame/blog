---
title: "Bash Search Text"
date: 2023-01-19T13:33:04-06:00
draft: false
thumbnailImagePosition: left
thumbnailImage: img/bash.png
coverImage: img/bash-header.png
metaAlignment: center
coverMeta: out
categories:
- DevOps
tags:
- devops
- linux
- open source
- bash
---

### Bash Search Text

Creating a bash script to collect specific text from a file is a relatively simple task that can be accomplished using a few basic command line tools. In this post, we will walk through the process step-by-step, so you can start collecting the text you need in no time.

First, open a text editor and create a new file. This will be the script file where we will write the commands that will collect the text from the target file.

Next, we will use the grep command to search for the specific text we want to collect. The grep command is used to search for patterns in text files and can be used to search for specific words or phrases. The basic syntax for the grep command is grep "pattern" file.

For example, let's say we want to collect all of the lines in a file that contain the word "example". We would use the following command:

```
grep "example" file.txt
```

You can also use regular expression to search for pattern in file, for example:

```
grep -E '^[0-9]+' file.txt
```

This will search for lines in file.txt that start with one or more digits.

You can also redirect the output of the grep command to a new file using the > operator. For example, to save the lines that contain the word "example" to a new file called "output.txt", we would use the following command:

```
grep "example" file.txt > output.txt
```

You can also chain multiple commands to perform different actions on the output, for example, you can use awk command after grep command to extract specific column from the lines that matched the pattern, for example, you can use:

```
grep -E '^[0-9]+' file.txt | awk '{print $2}'
```
This command will extract the 2nd column of the lines that matched the pattern.

And that's it! With just a few simple commands, you now know how to create a bash script to collect specific text from a file. You can now use this script to automate the process of collecting text from any file on your system.

Please note that these are basic examples of usage of the commands, you can find more advanced usage by visiting the official documentation of the commands.
