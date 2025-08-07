---
layout: default
title: Projects
not_post: true
---

On this page you'll find my projects, that I'd show to public.

I'm quite lazy, so there have been many projects that I've abandon and never finish, yet they are
more useful and complex than all this silly stuff below. One day I will return to them...

# Medium-size projects

Those projects took quite effort and I'm proud of them. But they are still probably useless.

## [monolog](https://github.com/inunix3/monolog)

Simple interpreted C-like imperative programming language. It was written as a school project in C.
It took exactly 1 month to write such language.

![monolog examples](/assets/images/project-showcase/monolog.gif)

It supports:

- Infix notation (`2 + 3 / 0`)
- Arithmetic (`+, -, *, /, %`)
- Logic (`!, ==, !=, <, >, <=, >=, &&, ||`)
- Basic branching statements (`if, else`)
- Loops (`while, for, break, continue`)
- Block statements
- Functions
- Builtin types:
    - 64-bit signed integers (`int`)
    - Mutable, resizable strings (`string`)
    - Option type (`T?`)
    - Array (`[T]`)
- REPL

It's really a simple language, usable only for academic problems.

The overall runtime process looks like this:

1. Lexing
2. Parsing
3. Semantic Check
4. Interpretation

The lexer is implemented in a procedural way, i.e. without any fancy looking state machines. Just
a `while` loop until EOF with `if`s for character + related function with another `while` loop. It
produces an array of tokens.

For parsing it uses the famous
pratt parser[^1]. I don't have too much experience with other parsing techniques, but I can
absolutely recommend this one.

The semantic check stage checks if there are no wrong combinations of types, symbol resolving, etc.

The interpreter is just a tree-walk one. Thanks to the previous stage, we are left only with
runtime errors, significantly simplifying the code of the interpreter.

![monolog repl](/assets/images/project-showcase/monolog_repl.gif)

For REPL I used a really good library [isocline](https://github.com/daanx/isocline). My only
complaint is, that its API for terminal styling is available only for stdout (it could be used
for diagnostics, and diagnostics should go to stderr).

## [nchip8](https://github.com/inunix3/nchip8)

CHIP-8/SCHIP interpreter written in C++17 using SDL2 and Dear ImGui. Customizable and has debug
capabilities.

<div class="image-row">
![screenshot 1](/assets/images/project-showcase/nchip8_1.png){: width="427" }

![screenshot 2](/assets/images/project-showcase/nchip8_2.png){: width="429" }
</div>

<div class="image-row">
![screenshot 3](/assets/images/project-showcase/nchip8_3.png)

![screenshot 3](/assets/images/project-showcase/nchip8_4.png)
</div>

I plan to rework this project - port it to Qt6, add editing and debug capabilities just like in
Mesen2 emulator and some kind of library, where you can choose game to play and each can have its own
defined properties like speed, quirks, etc. And also support XO-CHIP, of course.
In fact, I have some local code, but the school disrupted me and I've abandoned it. But I
will return to it.

It has a few bugs, which I fixed locally, but didn't pushed them to Github yet.

# Mini projects

These doohickeys were made because of boredom, have little/no practical use, but they're mine
and I had fun writing them.

## [rxpipes](https://crates.io/crates/rxpipes)

2D screensaver for terminals, written in Rust. It's basically rewrite of ncpipes, but cooler.

It has various features like setting drawing speed, RGB/palette, gradient, pipe char sets, etc.

One of interesting features it has is a **depth mode** - there are multiple layers of pipes, and
each layer gets darker until fully disappearing (can be seen on the right screenshot).

Not tested on Windows, but should work.

<div class="image-row">
![screenshot 1](/assets/images/project-showcase/rxpipes_1.png){: width="424" }

![screenshot 2](/assets/images/project-showcase/rxpipes_2.png){: width="425" }
</div>

## [ncpipes](https://github.com/inunix3/ncpipes)

2D screensaver for terminals, written in C + [notcurses](https://notcurses.com/).
Predecessor of rxpipes.

![ncpipes](/assets/images/project-showcase/ncpipes.gif){: width="60%" }

## [dshw](https://github.com/inunix3/dshw)

A dead simple CLI program to query information about system and some hardware. Written in Rust.
Uses the [sysinfo](https://crates.io/crates/sysinfo) crate for that.

```sh
~ $ dshw memory total available usage free
16680706048
11274551296
5406154752
4898979840
~ $ dshw drive /dev/sda3 fs usage total
ext4
259652198400
474853687296
~ $ dshw network enp0s31f6 total-transmitted-data
7632128
~ $ dshw list-sensors
acpitz temp1
acpitz temp2
coretemp Core 1
coretemp Core 5
coretemp Package id 0
coretemp Core 2
coretemp Core 4
coretemp Core 7
coretemp Core 0
coretemp Core 6
coretemp Core 3
amdgpu edge
nvme Composite WD Red SN700 1000GB temp1
~ $ dshw -d ', ' list-cpus
cpu0, cpu1, cpu2, cpu3, cpu4, cpu5, cpu6, cpu7, cpu8, cpu9, cpu10, cpu11, cpu12, cpu13, cpu14, cpu15
~ $ dshw -f '%usage%/%total% bytes' memory
8163627008/16689266688 bytes
~ $ dshw -f '%frequency%, %vendor-id%' cpu cpu7
3600, GenuineIntel
~ $ dshw help memory
Usage: dshw memory [QUERIES]...

Arguments:
  [QUERIES]...
          Possible values:
          - usage:     Total memory usage
          - total:     Total memory capacity
          - available: Reusable memory. On FreeBSD, it's the same as `free`
          - free:      Unallocated memory. On Windows, it's the same as `available`

Options:
  -h, --help
          Print help (see a summary with '-h')
```

## [raypong](https://github.com/inunix3/raypong)

Clone of Ping Pong written in C and [raylib](https://www.raylib.com/). Raylib is great for
old-school gamedev. For UI I used raygui.

![raypong](/assets/images/project-showcase/raypong.gif)

All graphics is made by raylib renderer, except the background in the main menu is a screenshot,
with some effects applied in [Aseprite](https://www.aseprite.org/).

But honestly, raygui I didn't like that much. It's too lightweight - lacks any sane layout system,
instead you have to manually specify positions and sizes, which is completely inflexible.
They have an editor for it ([rguilayout](https://github.com/raysan5/rguilayout)) that makes life
easier, but still not ideal.

I like the look of raygui.

## [wetris](https://github.com/inunix3/wetris)

A tetris clone written in C and [SDL3](https://www.libsdl.org/).

![wetris](/assets/images/project-showcase/wetris.png)

All the graphics was made by me in [Aseprite](https://www.aseprite.org/) and
[Gimp](https://www.gimp.org/),
sound effects in [MilkyTracker](https://milkytracker.org/) and
[Audacity](https://www.audacityteam.org/). Looks like some odd game from 2000s era, and
sounds enough old school!

Initially I wanted to use SDL2, but it does not support tile textures, so I went for SDL3,
which in that time was in pre-release state (although I didn't make use of tiling in the end).

SDL3 also comes with its own text engine, which is pretty powerful, but I wanted to try write my
own text renderer, so I reinvented the wheel.

## [tdl-clock](https://github.com/inunix3/tdl-clock)

ASCII analog and digital clock for terminal written in C. It uses
[TDL](https://github.com/celtrecium/tdl) for graphics, a curses-like library written by my old
friend.

![analog clock](/assets/images/project-showcase/tdl_clock_analog.gif){: width="45%" }

![digital clock](/assets/images/project-showcase/tdl_clock_digital.gif)

[^1]: See [this](https://matklad.github.io/2020/04/13/simple-but-powerful-pratt-parsing.html),
    [this](https://martin.janiczek.cz/2023/07/03/demystifying-pratt-parsers.html)
    and [this](https://journal.stuffwithstuff.com/2011/03/19/pratt-parsers-expression-parsing-made-easy/)
