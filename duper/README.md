# grab\_files

This program watches a directory that is producing some kind of files and grabs
a copy of the files, placing them in another directory

### Installing

Requires pyinotify

```
# With pip
pip install pyinotify

# For Centos:
yum install python-inotify
```

Then just copy the script to a directory in your path. Make sure it's got executable permission

```
cp grab_files /usr/local/bin/
chmod +x /usr/local/bin/grab_files
```

### Usage

grab\_files [ -i/--include include-pattern ] ... [ -e/--exclude exclude-pattern ] ... watch-directory destination-directory

- watch-directory
  Directory from which files are copied. The program watches for `CLOSE_WRITE` and `MOVED_TO` items from `inotify`. The directory is monitored recursively (i.e. sub-directories are also monitored).

- destination-directory
  Directory to which files are copied. If a file is copied from a sub-directory of the watch-directory, the same sub-directory is created at the destination.

- -i/--include
  Include only the specified glob patterns (shell style globs: "`*.log`"). By default, all patterns are included.

- -e/--exclude
  Exclude the specified glob patterns (shell style globs: "`*.log`"). By default, no patterns are excluded.

Include directives are checked first, then exclude directives.

It is possible for files to appear and then be removed faster than this program can open and copy them.

### Examples

1. Copy all files produced in /usr/tmp into ./tmp\_copy

```
grab_files /usr/tmp tmp_copy
```

2. Copy all files ending in .done as well as all files beginning with "sum_" from /var/lib/docker/volumes/output-logs/_data to ./output-logs:

```
grab_files -i '*.done' -i 'sum_*' /var/lib/docker/volumes/output-logs/_data output-logs
```


## Author

* **Jeff Barber**

