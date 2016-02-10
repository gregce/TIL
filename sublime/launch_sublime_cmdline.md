# Shortcut to launch Sublime from terminal

Are you on MacOSX? Are you a heavy Sublime text user?

You can easily configure a symlink to use to execute and open sublime
from terminal. 

Step 1: Test to see if the CLI is where it ought to be

```
$ open /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl  
```

Step 2: Assuming Step 1 worked, create a symlink to the CLI
```
$ ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl  ~/sublime
```

Step 3: Update your .bash_profile
```
$ nano ~/.bash_profile
$ export PATH=~/:$PATH
```

Step 4: Source your .bash_profile
```
$ source ~/.bash_profile
```

Step 5: Profit!
```
$ sublime filename
```
