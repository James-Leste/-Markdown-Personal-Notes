# Git & Version Control

## Tracking Files

- Staging files
```bash
    git add <filename1> <filename2> ...
    git add . # add all files in the root path
```

- Add a `.gitignore` to ignore files to be included
```bash
    # add suffix or filename that you don't want the git to track
    *.txt
    *.md
    *.py
```

- See `Difference` (**do it before staging**)
```bash
    # To see difference between before and after modification
    git diff <filename>

    # You can omit the filename to see all modifications
    git diff
```

- Unstage files (remove staged file from staging)
```bash
    git restore --staged <filename>
```

- Remove files (should be staged)
```bash
    git rm <filename>
```

- Rename files (should be staged)
```bash
    git mv <filename_original> <filename_target>
```

