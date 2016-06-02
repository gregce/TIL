#  Modifying how to log bash history

For anyone who is a frequent user of the command line (i.e. Terminal, etc), finding/greping your history for past commands can be either a monumental challenge or frankly impossible. While history does get logged to `/.bash_sessions`, it's not well organized.

One simple hack, shown below, can reduce the pain of searching your history

###  Add the following environment variable to your .bash_profile file

```
 export PROMPT_COMMAND='if [ "$(id -u)" -ne 0 ]; then echo "$(date "+%Y-%m-%d.%H:%M:%S") $(pwd) $(history 1)" >> ~/.logs/bash-history-$(date "+%Y-%m-%d").log; fi'
```
