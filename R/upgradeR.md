# Quickly upgrading Base R on Ubuntu

R is pretty easy to update in Windows from the R cli itself, the following three lines are all you need

```
install.packages("installr")  
library(installr)  
updateR()
```

Ubunutu is equally easy but the process is a bit different... In 5 lines with apt-get and the `$` you can do the same!

```
 sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9  
 sudo add-apt-repository ppa:marutter/rdev

```
 
and then

```
 sudo apt-get update  
 sudo apt-get upgrade  
 sudo apt-get install r-base r-base-dev  
```


)`
