
```

- git config --global user.name "user name"
- git config --global user.email email@email.com
- git config --global init.default branch "default branch name" //Usuially main
- git init //Initialize the local git repository
- git commit -m "Message" --amend //To change the previous commit message if needed
- git log --oneline //Print the previous commit on one line.Dont show the author 
- git reset commit-id //Erase last commit and jump back to desired commit-id
- git merge -m "message" branch-name // Merge from branch-name to the main branch
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