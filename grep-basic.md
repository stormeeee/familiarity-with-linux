# Understanding `grep`
+ grep is a command line tool which helps in filtering a file for specific piece of texts.
+ The grep filter searches a file for a particular pattern of characters, and displays all lines that contain that pattern. The pattern that is searched in the file is referred to as the regular expression.

## General Syntax
```bash
grep [options] [PATTERN to look for] [FILE in which to search for the pattern]

# put simple:
grep PATTERN file.txt
# >>> return all the lines that contains this pattern
```

## lets grep it!
### 1. To gather all the lines that have the search string "word":
```bash
grep "word" <file.txt>
```

### 2. To print the count of lines that have the search string "word" in a file:
```bash
grep -c "word" <file.txt>
grep --count "word" <file.txt>

# output
# integer number
```

### 3. To gather all the lines that **doesn't match** with the search string "word":
```bash
grep -v "word" <file.txt>
grep --invert-match "word" <file.txt>
```

### 4. To control the number of matching lines that has to be displayed:
```bash
grep "word" <file.txt> -m <maximum-number-of-lines-to-print>
grep "word" <file.txt> --max-count=[max-lines]
```
note: if the number of lines exceed the actual number of lines that match with the passed string, it will just list every single line, without raising any error!

### 5. To get the byte-level position of the first matching pattern from each line containing the pattern:
```bash
grep "word" <file.txt> -b
grep "word" <file.txt> --byte-offset

# outputs every line with byte-offset of the first matching in that line
```

### 6. To print the line number at which the line(printed in the terminal) is located in the file:
```bash
grep "word" <file.txt> -n
grep "word" <file.txt> --line-number

# start every line in output with its lines number in the file
```

### 7. If searching in multiple files, we can tell grep to print the file name as well from which the lines in the output are coming:
```bash
grep "word" <file.txt> <anotherfile.txt> -H
grep "word" <file.txt> <anotherfile.txt> --with-filename

# it can be combined with -n to print line number as well
```
### 8. In case of searching in multiple files, grep by default prints the filename as well from which the line is coming, we can tell grep to not print the filename:
```bash
grep "word" <file.txt> <anotherfile.txt> -h
grep "word" <file.txt> <anotherfile.txt> --no-filename
```

### 9. In case you are searching for a specific word or phrase in huge number of files, we can filter out the files in which the our "search-string" is present:
```bash
grep "word" <file.txt> <anotherfile.txt> ............ -l
grep "word" <file.txt> <anotherfile.txt> ............ --files-with-matches

# print the names of all the files that contains the passed string
```

### 10. In case you are searching for a specific word or phrase in huge number of files, we can filter out the files which don't contain the "search-string" also:
```bash
grep "word" <file.txt> <anotherfile.txt> ............ -L
grep "word" <file.txt> <anotherfile.txt> ............ --files-without-match

# print the names of all the files that doesn't contains the passed string
```

### 11. Sometimes, the file contents are soo long that it becomes hard to understand what the lines that are grepped are actually doing. In such a case, getting context becomes an easy thing by printing the lines around that particular grepped line. We can print context lines in three ways: 
```bash
# To get context lines after the matched line
grep "word" <file.txt> -A <number-of-context-lines>
grep "word" <file.txt> --after-context <number-of-context-lines>

# To get context lines before the matched line
grep "word" <file.txt> -B <number-of-context-lines>
grep "word" <file.txt> --before-context <number-of-context-lines>

# To get context line both before and after the matched line
grep "word" <file.txt> <number-of-context-lines>     
grep "word" <file.txt> -C <number-of-context-lines>
grep "word" <file.txt> -context <number-of-context-lines>
```

### 12. To search for patterns in a binary file
```bash
grep "pattern" <file.bin> -U
grep "pattern" <file.bin> --binary
```

### 13. To perform directory related operations:
```bash
# To search for a pattern in all the files that are present in a directory:
grep "pattern" -r .         # scans files in the current directory, including hidden files
grep "pattern" -r           # scans files in the current directory, excluding hidden files
grep "pattern" -r /path/to/the/directory
grep "pattern" --recursive
grep "pattern" -d recurse
grep "pattern" --directories=recurse

# When searching for a pattern in a directory containing files, we can choose to skip the inner-directories present in that directory:
grep -r -d skip "pattern" /path/to/the/directory
```

### 14. To know if a match to the pattern exists in a file, without knowing where it is,
```bash
grep "pattern" <file.txt> -q
grep "pattern" <file.txt> --quiet
grep "pattern" <file.txt> --silent
```

### 15. Finding patterns is an excellent choice when we don't know what we are exactly trying to find with full confidence. But in case we know what we are trying to search, we can use grep to search lines that exactly match your pattern:
```bash
# This will print all the lines that matches with your provided pattern from the start to the end
grep -x "pattern" <file.txt> 
grep --line-regexp <file.txt>

### 16. To perform pattern matching based on word boundaries, is also possible with grep. Word boundaries means that to search patterns that are surrounded by a white_space or a punctuation-mark. Example: assume a file containing two lines, one having "apple is my fav food" and the other having "I like pineapple the most......" ; when we perform word processing with pattern "apple" , only apple will be shown in output as it is a single entity whereas the apple from pineapple is a part of pineapple word as a whole.
```bash
grep -w "pattern" <file.txt>
grep --word-regexp <file.txt>
```

### 17. In many cases, we want that the pattern we are trying to search should not be matched exactly in terms of cases (lowercase, uppcase, defaultcase). We can do that this way:
```bash
grep -i "pattern" <file.txt>
grep --no-ignore-case "pattern" <file.txt>

note: by default, grep ignores cases, meaning, it will match the occurences, rather than matching exact case-based occurence. Therefore,
grep --ignore-case "pattern <file.txt> 		 #and
grep "pattern" <file.txt>			 # are the same
```

## Flavours of `grep`
+ There are many flavours of `grep` command-line utility, some of them are:
    1. `egrep` : works the same as `grep -E`
    2. `fgrep` : works the same as `grep -F`
    3. `pgrep` : used to grep the process ID

## Exit Status
+ Normally, if even a single pattern is found in the specified files/directory ; the exit status code will be 0, which denotes succesfull execution.
+ If no patterns were found, then 1 is returned.
+ If an error occurred, then 2 is returned.
+ and some others .........

## Notes:
+ The file name provided to grep is the standard input (stdin), if no stdin is given then `grep` will scan the current working directory.

# References
1. `grep -h`
2. `man grep` or [digital `grep` manual](https://www.gnu.org/software/grep/manual/grep.pdf)