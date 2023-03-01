## Archives
### tar
```bash
# create archive with files or/and dirs
# c -> create , z -> compress with gzip, v -> verbose, f -> name of archive
tar -czvf archive_name.tar.gz  file1 file2

# peek inside archive
tar -tf archive_name.tar.gz

# extract contents
# x -> extract
tar -xvf archive_name.tar.gz -C /path/to/dir
```
### zip
```bash
# create archive with files or/and dirs
zip  archive_name.zip  file1 file2

# peek inside archive
unzip -l archive_name.zip

# extract contents
unzip archive_name.zip -d /path/to/dir
```

### Practice:
- archive and compress some random 1MB file. Show the size difference.