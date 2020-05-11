# Common Git Commands

## Common

Create a repository, create the first commit and push it to the server:

```bash
echo "# Readme" >> README.md
git init
git add README.md
git commit -m 'initial commit'
git remote add origin [remote-address]
git push -u origin master
```

## Staging

### Add Files to the Staging Area

```bash
# Stage a single file
git add src/file.json

# Stage all files from the src folder
git add src

# You can even stage files using globs
git add src/*.json

# Or you can stage just all files:
git add -A
```

### Check Staging Area

```bash
git status
```

This command applies to other use cases as well. You can see if there are any commits left to be pushed, if there are any changes to your files or if your branch is behind the origin branch.

## Commit changes

```bash
# Basic commit
git commit -m 'commit message'

# Commit with simultaneously staging the changed files
git commit -am 'commit message'

# Modify the previous (unpushed) commit to add additional changes
git commit --amend
```

## Branching

```bash
# View all local branches
git branch

# Switch to a branch
git checkout [branch-name]

# Create a new branch and check it out
git checkout -b [new-branch-name]

# Switch back to the previous branch
git checkout -
```

## Working with the Remote

```bash
# Check if the remote has anything new for me
git fetch

# Push changes to Remote
git push

# Get changes from Remote
git pull

# View available origins
git origin -v
```

## Debugging

### View Complete Log

```bash
git log
```

### Use Git Bisect

```bash
# Start a bisect session
git bisect start

# Tell git that this commit is bad
git bisect bad

# Tell git that this commit is good
git bisect good

# Tell git about a particular good commit
git bisect good 005b4e6aa757a5c8c08aa694c01e630631b6aaba

# Reset after bisect session
git bisect reset
```
