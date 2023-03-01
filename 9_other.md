## crontab

For recurrent tasks, linux provides a daemon that can run scripts based on a fixed schedule defined with ```crontab -e```.
You will find the syntax in the opened file.

### Practice:
- add an entry to write to a file the current datetime. The file must hold a maximum of 10 lines. Will determine the recurrence on the spot.

## sed

sed is used mainly to replace strings that match a pattern with another string

### Practice:
- replace all characters "#" with "$" in the lesson files, then undo the change

## awk
awk is used for text processing and formatting 

### Practice:
- get all strings from all lesson files that have at least one "#" before it. They will be mainly lesson titles and practice key-word