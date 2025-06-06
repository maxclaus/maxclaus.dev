+++
title = "Vim - Open several files at once"
description = "How to open several files at on in Vim"

# [extra]
# [extra.shared]
#   LinkedIn = ""
#   Reddit = ""
+++

Last week I had to make changes to several files at once. In order to have all those files
open at once in VIM I used this interesting approach described below, which I found in
[this Stackoverlfow question][stackoverflow_question].

I grabbed the list of files and saved them to a `files.txt` file, each file
must be in a new line and prefixed with `e` (edit) command:

```
e file1.js
e file2.js
```

Then in vim run:

```
:so files.txt
```

Each file will be open in a different buffer.
Then, as changes have been done to each file, run `:w|bd` to save the current file, close the current buffer and move to the
next buffer.

[stackoverflow_question]: https://stackoverflow.com/questions/2023191/how-can-i-open-several-files-at-once-in-vim
