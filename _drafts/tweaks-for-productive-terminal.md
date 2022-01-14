---
layout: post
title: "5 Tweaks for a productive Terminal"
author: Roy Straub
categories: [Tools]
tags: []
image: assets/images/construction.jpg
description: "The terminal is a developer's best friend. In this post, we'll look at five ways to make the terminal an even better companion to your workflow."
featured: true
hidden: true
comments: true
---

The terminal is a developer's best friend.
In this post, we'll look at five ways to make the terminal an even better companion to your workflow.

## Why Tweak Your Terminal?

* Spend tons of time in terminal
* Make the tool work for you

## A Turbocharged Terminal Emulator

A [Terminal Emulator](https://en.wikipedia.org/wiki/Terminal_emulator) is the application you use to interact with your shell.
Your OS comes with a default terminal, and they can be pretty good.
The thing is there are more powerful "aftermarket" options to be found. 

One such option is [Kitty](https://sw.kovidgoyal.net/kitty/), another great one is [Alacritty](https://github.com/alacritty/alacritty).
I've used Kitty the most, and have come to prefer it, so let's have a look at what it can offer over a standard terminal application.

Kitty is an open source terminal emulator with some standout features:
* *GPU Rendering.* Offloads rendering to the GPU for a smoother experience and freeing up the CPU to do its job quicker.
* *Versatile Rendering.* Kitty supports rendering of glyphs, emoji, ligatures and has great font support out of the box.
* *Tabs and multiplexing.* Multitasking is very effective with Kitty, as it supports tabs and multiple windows in a single tab.
* *Keyboard-driven.* As a power user, the keyboard is your friend. Kitty embraces this philosophy and is almost entirely driven with sensible keyboard shortcuts.
* *Extensible.* Kitty supports plugins, which it calls [kittens](https://sw.kovidgoyal.net/kitty/kittens_intro/?highlight=kitten#). It is also [scriptable](https://sw.kovidgoyal.net/kitty/remote-control/?highlight=script) at its core!
* *Configurable.* Don't like a keybinding or how something works? Change it! A tool should fit your workflow, and Kitty allows you to do just that.

For me the responsiveness, great rendering experience and productivity enhancements make a great difference in terminal work.
Another big factor to productivity in the terminal is the shell.
Let's see how we can give that an upgrade.

## A Superior Shell

The [shell](https://en.wikipedia.org/wiki/Shell_(computing)) is crucial to your terminal experience, because it is always present.
It is what you use to interact with your Operating System.

You're probably familiar with the [_Bash_](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) which comes as a default to many Operating Systems.
But, same as with the emulator, there are more powerful options around.
The shell I would recommend nowadays is [_Fish_](https://fishshell.com/).

What makes Fish great? It offers great productivity boosters like:
* **Autocompletion.** Like code completion, but for terminal commands. After a while Fish becomes almost telepathic, and you hardly have to type commands at all!
* **Man page completion.** Ever wondered which flags are available for a specific CLI? Fish can show you inline hints and descriptions based on the [man pages](https://en.wikipedia.org/wiki/Man_page) for the command.
* **Color support.** Fish supports 24 bit colors, which is really helpful in practice. For instance Fish colors anything you type in the terminal, letting you know whether a command is valid (blue) or not (red) before you've even run it!
* **Out-of-the-box experience.** Some other shells can get some of these features working, but it requires a lot of tinkering. Fish is great out of the box, and doesn't take up any unnecessary time to set up.
* **Plugins.** If you do like to tweak your shell, you can do so with Fish. The projects [Fisher](https://github.com/jorgebucaran/fisher) or [Oh My Fish](https://github.com/oh-my-fish/oh-my-fish) offer great plugin support. For instance I run a plugin that gives me a lot of sane aliases for using the git CLI.

Fish helps you do what you need to do in the terminal in a much more efficient manner, but we can do better!
Besides the shell we can also make the prompt be more useful to us.

## A Powerful Prompt

What is a prompt?
It's (usually) the `$` sign that tells the user whether the CLI is ready to accept a new command.
Doesn't sound too spectacular, now does it?

We can make it do much more by installing a prompt like [Starship](https://starship.rs/).
Starship transforms your prompt and makes it display relevant information based on the directory you're in.

Some of the useful things it can show are:
* **Git status.** This shows the current branch, and information about the status of the repository like whether it has uncommitted changes or is behind the remote. 
* **Exit code status.** Clear indicators and exit codes of the previous command.
* **SDK info.** Starship can show the current version for Node.js, Java, Python, and many more if it detects corresponding project files. Especially useful when those projects have specific SDK requirements!
* **Cloud and Docker contexts.** Shows you all kind of information about the current contexts of cloud technology, like the current Kubernetes context.
* **Much more...** Honestly, there is so much more Starship can do. You can even show things like current ram usage, or battery percentage. Configuring it is a breeze, so experiment away.

I have come to rely on this little piece of software quite a bit. It's very neat to have so much information always at your disposal in the terminal. Saves me typing a ton of commands!

Great, we've now go a very potent terminal stack already, what more can we improve? Up next, is the multitasking experience.

## Multitasking with Multiplexing

How often do you run multiple, or long-running commands in the terminal? I often run development servers, test tasks or software installations a lot. Wouldn't it be great if you could do all those things effectively?

Multiplexers are amazing for these use cases. [_Terminal Multiplexing_](https://en.wikipedia.org/wiki/Terminal_multiplexer) is rendering multiple terminal sessions in a single window. Kitty offers this out of the box, but there are standalone options like [tmux](https://github.com/tmux/tmux) dedicated to this task.

They generally offer support for rendering multiple tabs and windows within tabs. On top of this, they also allow you to personalize your layouts to just the way you like it.

I use multiplexing to run commands that take a long time simultaneously without losing focus. Gone are the days where I open six terminal instances or tabs. Multiplexing allows me to group relevant processes in one view.

Lastly, let's have a look at optimizing one of the most common tasks in the terminal: issuing commands.

## Keyboard Wizardry with Vim Keybindings

Don't you hate it when you have a command in your terminal, but you need to change just a few parts of it. This tedious work usually involves pressing the arrow keys until you reach the part of a command you wish to change. Not necessary!

If you are familiar with the keybindings of [Vim]() this might be interesting for you. With a little tweaking, you can set up Vim keybindings for your shell. In Fish, all that's required is to add `fish_vi_key_bindings` to your config file (usually in `~/.config/fish/config.fish`.

What this allows you to do is to enter _Normal_ mode to navigate text in commands just like you're used to in regular Vim. It also makes navigating command history more ergonomic, as you can use the `j` and `k` key in `normal mode` to select previous or next commands. Never leave the [home row](https://en.wikipedia.org/wiki/Touch_typing#Home_row) on your keyboard again!

## Putting it all together

Any of these tweaks can help your terminal workflow improve, but they work even better in tandem. 

Starship's prompt is beautifully rendered, with colorful emoji in Kitty. Fish is blazing fast, as is Kitty. Multiplexing requires zero setup in Kitty, and is extremely smooth. Lastly both Vim and Kitty's keybindings are ergonomic and effective.

## Conclusion

The terminal is one of the most commonly used tools for a developer. In this post I showed you how to make that tool even more effective with a few minor tweaks.

By using a better **emulator** you can elevate your terminal experience, and a better **shell** allows you to run commands more effectively. An upgraded **prompt** shows you useful information at a glance, whilst **multiplexing** can make your multitasking workflow smoother. Lastly, setting up proper **keybindings** simplifies the manipulation of commands.

Invest a little bit of time into your terminal setup, it will pay dividends!

_What is your preferred terminal workflow? Any tips for an even better setup? Share your thoughts in the comments below!_

