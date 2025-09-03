
```

- git config --global user.name "user name"
- git config --global user.email email@email.com
- git config --global init.default branch "default branch name" //Usuially main
- git init //Initialize the local git repository
- git commit -m "Message" --amend //To change the previous commit message if needed
- git log --oneline //Print the previous commit on one line.Dont show the author 
- git reset commit-id //Erase last commit and jump back to desired commit-id
- git merge -m "message" branch-name // Merge from branch-name to the main branch
- git branch -d branch-name //To delete a branch
- git branch -d branch-name // Delette the branch with the name "branch-name" 
- git push --all //Push changes from all branches
- git pull // fetch and merge files from the git-cloud to the local directory.
 

```

 
# Merge conflict

Merge conflict happens when you try to merge to the parent branch that was changed from some one else. 

To solve them check the content of conflicting files and compare them. Decide what version you need and erase the undesired information.

  Push and that is all.
 
# What is a pull request
  
When a change has to be reviewed by someone in oder to approve the change to be merged into the main.


## Git Prompt Settings

- Step 1: Clone the git repository as shown below
    

`git clone https://github.com/magicmonty/bash-git-prompt.git ~/.bash-git-prompt --depth=1`

- Step 2: Open your .bashrc file using your preferred editor i.e. nano
    

`nano ~/.bashrc`

- Step 3: Copy the following lines and paste at the end of your .bashrc file and save
    

`# Set config variables first GIT_PROMPT_ONLY_IN_REPO=1 # GIT_PROMPT_FETCH_REMOTE_STATUS=0 # uncomment to avoid fetching remote status # GIT_PROMPT_IGNORE_SUBMODULES=1 # uncomment to avoid searching for changed files in submodules # GIT_PROMPT_WITH_VIRTUAL_ENV=0 # uncomment to avoid setting virtual environment infos for node/python/conda environments # GIT_PROMPT_VIRTUAL_ENV_AFTER_PROMPT=1 # uncomment to place virtual environment infos between prompt and git status (instead of left to the prompt) # GIT_PROMPT_SHOW_UPSTREAM=1 # uncomment to show upstream tracking branch # GIT_PROMPT_SHOW_UNTRACKED_FILES=normal # can be no, normal or all; determines counting of untracked files # GIT_PROMPT_SHOW_CHANGED_FILES_COUNT=0 # uncomment to avoid printing the number of changed files # GIT_PROMPT_STATUS_COMMAND=gitstatus_pre-1.7.10.sh # uncomment to support Git older than 1.7.10 # GIT_PROMPT_START=... # uncomment for custom prompt start sequence # GIT_PROMPT_END=... # uncomment for custom prompt end sequence # as last entry source the gitprompt script # GIT_PROMPT_THEME=Custom # use custom theme specified in file GIT_PROMPT_THEME_FILE (default ~/.git-prompt-colors.sh) # GIT_PROMPT_THEME_FILE=~/.git-prompt-colors.sh # GIT_PROMPT_THEME=Solarized # use theme optimized for solarized color scheme source ~/.bash-git-prompt/gitprompt.sh`

- Step 4: Source your .bashrc file
    

`source ~/.bashrc`



## Figlet

```
figlet Silvere # The output can be copied to the bahrc so after each terminal start 

Output:


```

## Turn off VS-Code Sound 

![[Pasted image 20250808105853.png]]