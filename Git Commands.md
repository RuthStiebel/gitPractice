### Initializing a Repository
```bash
git init                                # Create a new Git repository
git clone <repository_url>              # Clone an existing repository from a URL
git clone --bare <file_to_create>       # Create a bare git folder
```

### Working with File Changes
```bash
# Check project status
git status                               # Current status of the project
git ls-tree HEAD                         # View all files in the latest version
git ls-tree <commit_id>                  # Files committed in a specific commit
git ls-files --stage -- <file_name>      # Files in the staging area
git ls-files --others                    # List untracked files
git ls-files --exclude-standard          # List tracked files, excluding ignored ones

# View and compare changes
git diff                                 # Show unstaged changes
git diff --cached                        # Show staged changes
git diff <commit1> <commit2>             # Show differences between two commits

# Viewing differences
git diff <branch_name>                                  # View differences between the branch and HEAD
git diff <branch_name> <branch_name>                    # Show differences between two branches
git difftool -d <branch_name> <branch_name>             # Use a graphical tool to show differences in directory
git difftool <branch_name> <branch_name> -- <file_name> # Use a graphical tool to show file differences
git diff --summary <branch_name> <branch_name>          # Compare two branches and show a summary

# View specific commit details
git show <commit_id>                                                # Show details of a specific commit
git cat-file commit <commit_id>                                     # See author details for a specific commit
git cat-file commit HEAD                                            # Show the latest commit details
git cat-file commit HEAD^                                           # Show details of the commit before the last
git cat-file commit HEAD~<num>                                      # Show commit X numbers before HEAD
git cat-file blob <file_num>                                        # View file contents in a specific commit
git blame -- <file_name>                                            # See who modified each line in the specified file
git blame <commit_id> -- <file_name>                                # Blame a specific commit on a file
git blame --reverse <from_commit_id>..<to_commit_id> -- <file_name> # See the last revisions where a line appeared between commits
```

### Staging and Committing Changes
```bash
# Stage files for commit
git add <file_path>                     # Add a specific file
git add .                               # Add all files in the current directory
git add -A                              # Stage all changes (tracked and untracked)

# Commit changes
git commit                              # Commit staged changes
git commit -a                           # Commit and add all
git commit -m "Your commit message"     # Commit with a message
git commit --amend                      # Modify the last commit (message or files)
git commit --allow-empty                # Create an empty commit (useful for triggering CI/CD)
git commit --author="Name <email>"      # Specify a different author for the commit
git commit --no-edit                    # Commit with the previous commit message
```

### Viewing Commit History
```bash
git reflog                              # See all past commits, including branches
git log                                 # View all past commits (excluding branches)
git log --graph                         # Display the commit history as a graph
git log --oneline                       # View past commits in one line per commit
git log --follow -- <file_name>         # View commit history for a specific file
git log -n <num> -- <file_name>         # See a specific number of past commits on a file
git log -p <commit_id>                  # View changes in a specific commit
git log -S '<phrase>'                   # See commits that modified a specific phrase
git log -- <file_name>                  # View commits that modified a specific file
git log <branch_name>                   # View commits that modified a specific branch
git log --before=<num>.days             # Show commits before the specified number of days
git log --since=<num>.days.ago          # Show commits since the specified number of days
```

### Modifying Files
```bash
# Resetting files
git reset <commit_id>                               # Move HEAD to the specified commit without changing files
git reset --hard <commit_id>                        # Move HEAD and reset all local files to the specified commit
git reset --soft                                    # Move HEAD without changing local files
git reset <file_name>                               # Remove a file from staging
git reset <file_name> + git checkout <file_name>    # Recover file from the beyond
git rm <file_name>                                  # Delete a file from the project
git rm -r --cached <folder_name>                    # Remove a folder without deleting it locally
git mv <original_file_name> <new_file_name>         # Rename a file and stage the change
git clean -f                                        # Remove untracked files from the working directory
git clean -nd                                       # Remove all untracked files
```

### Branching and Merging
```bash
# Branching
git branch                                   # List all branches
git branch <branch_name>                     # Create a new branch
git branch -d <branch_name>                  # Delete a local branch
git branch -D <branch_name>                  # Force delete a local branch
git branch -f <branch_name> <commit_id>      # Forcefully move a branch to a specific commit
git branch <branch_name> <commit_id>         # Create a branch from a specific commit
git branch <branch_name> -u <upstream>       # Define upstream branch for the specified branch
git branch --all                             # List all branches
git branch -VV                               # Show where the branch merges

# Checkout
git checkout <branch_name>                   # Switch to a specific branch
git checkout -b <branch_name>                # Create and switch to a new branch
git checkout <commit_id>                     # Switch to commit (detached HEAD state)
git checkout <branch_name> <commit_id>       # Copy file from specified commit to repository

# Merging
git merge <branch_name>                      # Merge a branch into the current branch
git merge --abort                            # Abort a merge in progress
git mergetool                                # Open a merge tool for conflict resolution
git merge-base <branch_name> <branch_name>   # Find the most recent common ancestor between two branches
```

### Patch and Cherry-Picking
```bash
# Creating and applying patches
git format-patch <commit>               # Create a patch for a specific commit
patch <patch_name>                      # Apply the changes from a patch file

# Cherry-picking commits
git cherry-pick <commit>                # Apply a specific commit from one branch to another
```

### Remote Repositories
```bash
git remote add <remote_name> <url>      # Add a new remote repository
git remote -v                           # View remote repositories
git remote add origin <url>             # Set the remote repository as 'origin'
git remote remove <remote_name>         # Remove a remote repository
git remote update                       # Fetch all remotes

# Fetch
git fetch                               # Fetch changes from a remote repository
git fetch <remote_name>                 # Fetch changes from a specific remote
git fetch --prune                       # Remove any remote-tracking branches that no longer exist on the remote

# Pull
git pull                                             # Fetch and merge changes from a remote
git pull <remote_name> <branch_name>                 # Fetch and merge changes from a remote repository

# Push
git push                                             # Push changes to a remote repository
git push <remote_name> <branch_name>                 # Push changes to a remote repository
git push --set-upstream <remote_name> <branch_name>  # Set upstream for the current branch

# Keys
ssh-keygen.exe -t rsa                   # Generate SSH key
cat ~/.ssh/id_rsa.pub                   # Get public SSH key
```

### Stashing Changes
```bash
git stash                               # Stash changes in the working directory
git stash save 'message'                # Save to stash with message
git stash list                          # List all stashed changes
git stash apply                         # Apply the latest stashed changes
git stash pop                           # Apply and remove the latest stashed changes
git stash pop <save_id>                 # Apply and remove the specified stashed changes
git stash drop                          # Remove a specific stash
git stash clear                         # Clear all stashes
```

### Rebasing
```bash
git rebase <branch_name>                # Reapply commits on top of another base branch
git rebase -i <base_commit>             # Interactive rebase to edit commits
git rebase --interactive <HEAD~num>     # Interactive rebase to edit commits
git rebase --abort                      # Abort an ongoing rebase
git rebase --continue                   # Continue rebasing after conflict resolution
```

### Configuration
```bash
git config --global user.name "Your Name"          # Set global username
git config --global user.email "you@example.com"   # Set global email
git config --list                                  # List all configuration settings
git config --global core.editor <editor>           # Set default editor for Git
git config --global alias.<shortcut> '<command>'   # Create aliases for common commands
git config --edit --global                         # Configure global settings (follow instructions on screen)
```

### Useful Aliases
```bash
# Creating aliases for frequently used commands
git config --global alias.co checkout              # Shortcut for checkout
git config --global alias.br branch                # Shortcut for branch
git config --global alias.ci commit                # Shortcut for commit
git config --global alias.st status                # Shortcut for status
git config --global alias.lg "log --oneline --graph --decorate"  # For pretty compact history view
```

### Advanced Features - not covered in course
```bash
# Advanced usage
git bisect start                           # Start bisecting to find a bug
git bisect bad <bad_commit>                # Mark a commit as bad
git bisect good <good_commit>              # Mark a commit as good
git bisect reset                           # End bisecting
git submodule add <repository_url> <path>  # Add a git submodule
git submodule update                        # Update all submodules
```

### Tags - not covered in course
```bash
git tag                                 # List all tags
git tag <tag_name>                      # Create a new tag
git tag -a <tag_name> -m "message"      # Create an annotated tag with a message
git push origin <tag_name>              # Push a specific tag to the remote repository
git push origin --tags                  # Push all tags to the remote repository
git show <tag_name>                     # Show details of a specific tag
```

### Miscellaneous Commands
```bash
# Navigating directories and viewing files
cd <folder_name>         # Go to child folder
cd ..                    # Go back to the parent folder
ls                       # Show contents of the directory
ls -a                    # Show hidden files
dir                      # Show contents in Windows
touch <file_name>        # Create new file in directory
ech 'text' > <file_name> # Write text in specified file
cat .gitconfig           # See git configurations
vi <file_name>           # Opens file for editing (text editor, more advanced)
nano <file_name>         # Opens file for editing or creates new one if it doesn't exist
```

### AHHHHHHHHHHHHHHHHHHH Oops
```bash
# Added wrong file to staging area
git status -> git ls-files --stage -> 
git reset --<file_name> -> git clean -f <file_name>                   

# Committed wrong files
git reset --soft HEAD^ -> git status ->
git reset <wrong_file_name>  

# Forgot to create branch
# Noticed after saving but before committing and adding 
git checkout -b <new_branch_name>

# Noticed after commit
git reset --hard HEAD^ -> git branch <new_branch_name> <commit_id> ->
git checkout <branch_name>  
```