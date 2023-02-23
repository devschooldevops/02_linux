# Shell basics

``` bash
touch file              # create empty file
mkdir dir               # create empty dir

rm file                 # delete file
rmdir dir               # remove empty dir
rm -r dir               # remove dir with all its contents recursively

ls                      # list dirs and files in current dir
ls -a                   # list everything, including hidden files and dirs

pwd                     # print working dir

cd dir                  # navigate inside dir
cd ..                   # go back (up)
cd                      # go home :)
cd ~                    # same as above, go to current user home dir
cd $HOME                # go to current user home dir

cp file1 file2          # copies file1 to file2
mv file1 file2          # moves (renames) file1 to file2
# cp and mv can also be used recursively for dirs

echo "Hello world!"

cat file                # display file content

man command             # display manual entry for command

# use <tab> to autocomplete commands

# Ctrl + r <term>       # search in previous commands (in history)
history                 # display shell history

# Ctrl + Shift + C      # copy selected text from terminal
# Ctrl + Shift + V      # paste in terminal where the cursor is
```