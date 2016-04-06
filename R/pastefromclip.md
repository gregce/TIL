# Reading data in from the clipboard on mac

The function readClipboard doesn't behave on Mac (when compared to Windows machines). Never fear, however; as leveraging the pipe can provide for an equally terse solution

```
data <- read.table(pipe("pbpaste"), sep="\t", header=T)
```

More details on these command line functions can be found here[https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/pbpaste.1.html]