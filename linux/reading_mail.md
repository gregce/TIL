# Combing and Zipping w/ Tar and Gzip

Its common the case that you want to combine / archive a bunch of files together prior to compressing them. Using standard bash, this is made possible through the use of tar + gzip. 

### Archvie and zip in a single line

```
$ tar -czvf file.tar.gz myfiles*.txt
```

###  Unzip later on

```
$ tar -xvzf file.tar.gz -C /path/to/parent/dir
```
