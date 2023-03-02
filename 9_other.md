## crontab

For recurrent tasks, linux provides a daemon that can run scripts based on a fixed schedule defined with ```crontab -e```.
You will find the syntax in the opened file.

### Practice:
- add an entry to write/overwrite the current datetime to a file. Recurrence to be decided.

## sed

sed is used mainly to parse and transform text

### Practice:
- replace all characters "#" with "$" in a lesson file, then undo the change (or don't save it at all)

## awk
awk is used for text processing and formatting 

### Practice:
- get the words from a lesson file that have at least one "#" before it. They will be mainly lesson titles and practice key-word.