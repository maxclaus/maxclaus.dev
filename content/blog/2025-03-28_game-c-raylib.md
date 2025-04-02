+++
title = "Building a Game in C"
description = "Building a game in C with raylib library"

# [extra]
# [extra.shared]
#   LinkedIn = ""
#   Reddit = ""
+++

After diving into Assembly programming, which I mention in my previous post, and gaining a better understanding of the basics of how programs work on a lower level.
I decided it was time to move one level up and get some experience with [C][c_lang]. So I built a tiny game as my first
project.

Some interesting points about C programming:

1. C was first released in 1972. The latest stable release was in 2024 (C23), but it seems most projects are still using C99 from 1999.
2. The [standard library][c_std_lib] is quite minimal. For instance, there is no built-in http server, you either need to build it
   from scratch or rely on an external library. Typing and data structures are also minimal. For example,
   there is no dynamic resizable arrays (a.k.a. vector), so once again, you either need to implement them yourself or use an external library.
3. No garbage collector. For memory stored in the stack, the compiler takes care of managing the memory automatically. However,
   dynamic memory, which is stored in the heap, must be managed manually using functions like `malloc`, `realloc`, and `free`.

Some engineers might consider those points a drawback. However they also can be an advantage depending on your goal.
Based on the previous points:

1. Most projects still using C99 because it is good enough for what they need. It also keeps compatibility with wider range of other projects that are on C99 too.
2. A minimal standard library is a good thing for those looking to build a small library/program. For instance, many projects using C run on
   embedded systems, and even the standard library could be something they don't need. For more reasons,
   check out [this Reddit thread][reddit_c_std_lib].
3. No garbage collector running on a program means less overhead, as the memory management where data is allocated and
   free is known at compile time.

About the game, it uses [raylib][raylib], a simple library which makes programming video games quite enjoyable. Basically, the game engine works by
re-drawing elements (e.g. pixel, shape, texture, and etc.) on every frame update. On each new frame, the screen is clean and
the re-drawn happens again, reflecting the current state of the game, such as a character moving or reacting to
collisions.

In addition to rendering graphics, the game also includes sound effects, making the experience more engaging.

Although the game was written in C, it targets both Desktop and Web platforms. The web version compiled to WebAssembly and can be
played online at [maxclaus.itch.io/falling-world][game_url].

Check out the [source code][repo_url] of the game if you are interested.

At the end, I found super cool coding it in C, and working with dynamic memory allocation was particular interesting. I am excited
to experiment more with C in future side projects.

[c_lang]: https://en.wikipedia.org/wiki/C_(programming_language)
[raylib]: https://www.raylib.com/
[c_std_lib]: https://en.wikipedia.org/wiki/C_standard_library
[reddit_c_std_lib]: https://www.reddit.com/r/C_Programming/comments/iqtvde/why_are_data_structures_not_part_of_the_standard/
[game_url]: https://maxclaus.itch.io/falling-world
[repo_url]: https://github.com/maxclaus/raylib-game
