+++
date = "2015-11-06T16:55:21+08:00"
title = "Square peg into a square hole"

+++

# Go

My friends know me as someone who is not very loyal. I don't mean to my girlfriend. I mean to various technology and web stacks. Ever since the advent of node.js, frameworks, tooling and just weird stacks have popped up. Not that I'm complaining.

My current interest is in [Go](golang.org), or [Golang](golang.org). I won't bother introducing it here, as I'll just be repeating what others have said.

I've been really interest in the language lately, and I look forward to building apps with it. One of the main limitations of Go at the moment is the lack of a proper UI library. There are some bindings to GTK/QT somewhere, but usually filled with bugs or some weird hackery.

# Electron

I have also been looking into [Electron](http://electron.atom.io/) lately. It used to be known as Atom Shell and has been rebranded recently.

Electron allows people who are more experienced in Single Page App (SPA) style development to build apps for desktops. All signs point towards web apps as the future, but yet here is Electron and Atom enjoying success and adoption. It helps us lowly web developers to get our feet wet in desktop development.

A quick read of Electron documentation suggests that it runs off a basic node.js server as the `main process`. There are also many `renderer processes` that can be spawned, and these will be your browser instances that will be presented to the end user.

Communication between the main and renderer processes are done by way of the ipc package that comes with Electron. So I'd imagine your main process handles most of the comms, state, and processing. One of the biggest complaints about node js is that when it blocks, it *really, really* blocks. Single threaded execution means that as soon as you do some sort of heavy number crunching you're screwed, and then everyone will start complaining about how your [app](http://atom.io/) is slow as molasses.

# Multi tier architecture
So why not defer the processing intensive stuff to yet another process? Perhaps using another language that is well suited to portability (static binaries) and performance.

There is something called [multitier architecture](https://en.wikipedia.org/wiki/Multitier_architecture) that allows one to split up these concerns cleanly. 

I have explored connecting a Go backend into Electron and have found reasonable success. The first iteration used a REST API, and my second attempt covers using gRPC instead, to great effect. I may have solved two problems in two different camps:

1. Performance by the main process in Electron
2. A UI toolkit for Go

I'll continue these musings in part two.
