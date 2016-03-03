# Tmux is a great multiplexer!

Similar to GNU screen, TMUX is a great way to split terminal screens and manage sessions. It lets us use a single environment to launch multiple terminals, or windows, each running its own process or program. This can be extremely useful for development on remote machines.

This TIL will expose the basics of TMUX usage from install to session management.

*Assumes MacOSX*

### Install tmux w/ Homebrew

```
$ brew install tmux
```


### Check that it's there

```
$ tmux -V
tmux 2.1
```

### Commands to get you up and running
Anything denoted with ^B means `ctrl+B`

```
## Start tmux
$ tmux

## split your pane
^B % 

## split your new screen horizontally
^B "
```

### Moving around and using tmux

```
## Move up one pane
^B <UP ARROW>

## execute a process
$ top

## maximize the process running in the current pane
^B z
```


### More windows!

```
## create a new window

^B c

## switch back to original window

^B 0
```

### Exiting, Listing, Killing and Reattaching 

```
## exit your session

^B d

## list sessinos

$ tmux ls

## kill a session

tmux kill-session -t 0 #t=target

## reattach to a session listed

tmux attach -t 1
```


