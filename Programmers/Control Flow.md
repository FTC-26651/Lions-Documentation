# Control Flow

This page is mostly by .frozenmilk from the FTC Discord, the original message is [linked here](https://discord.com/channels/1443377051305508896/1444893479519129600/1493801490379440301)

Command frameworks provide an implementation of the command based paradigm, which is an approach to control flow and concurrency:

## Control Flow
Control flow is the ability for the code to control "what happens next" the simplest example is an `if` statement, which decides based on `true` or `false` which block of code to run. command based libraries typically reimplement most of the basic control flow constructs of java, along with some more complex control flow constructs that work with the concurrency aspects of the library. 

## Concurrency
Concurrency is running multiple things in parallel. Command based frameworks provide a way to slice sequences of code (instructions / operations that should happen in order) and interleave them with other sequences, while still running on only one thread. This is the main challenge of commands, and allows you to have multiple things happen at once on your robot, each of which can still be written as though it happens in order by itself. Commands make it easy to do multiple things in parallel and wait for them, or to race things together, or cancel running processes, or have running processes interact with shared resources.

## Why?
As you write more robotics code you'll find that you want some way to run multiple things at the same time, that are each somewhat independent of each other. e.g., raise an arm, then open a claw, wait 0.5 seconds, then lower the arm, but while you raise the arm you drive to a position, then after you open the claw, drive away. this complex behaviour is very hard to model without some tools to manage the lifecycles of each step in the process, and to make sure they behave.

## Other Approaches
A simpler approach would be to use threads, which I would highly recommend against, as they don't provide many useful features and utilities, and make it very easy to introduce bugs into your code.

Nothing I have talked about here is particularly specific to Commands or their frameworks, there are other similar ways to achieve similar things, like RR Actions, or finite state machines (although these are much more limited, and don't have many of the other nice features). Commands are still the most popular way to write concurrent robot code however.

## Finite State Machines
What most low levels teams do, is to use a `switch` statement for a finite state machine. However, they have issues with scope pollution, poor guarantees, poor composability, and resuability.

Using a Finite State Machine well will require enumerations. However, since commands are much more popular and FSM's don't have nearly as much abstraction as Commands do, we use Commands

## Options:
SolversLib (Replaces FTCLib)
NextFTC
Ivy
RR Actions
Mercurial (Kind of, though not really)
(sorry if I left anyone out here)

--
[Previous Page](https://github.com/FTC-26651/Lions-Documentation/blob/main/Programmers/Libraries.md)