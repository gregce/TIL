#Shell magic to save time pushing changes to github

This TIL could be filed under linux or git but git feels more applicable.

Do you ever get in the habit of rapidly iterating on file(s) in a directory where you're interesting in adding, committing and pushing changes in rapid succession?

If so, a short shell sh script could possible save a lot of time / repetition

Step 1: Define that puppy
```
function lazygit() {
    git add .
    git commit -a -m "$1"
    git push origin master
}
```

Step 2: Assuming MacOSX, add to .bash_profile

Step 3: `source ~.bash_profile`