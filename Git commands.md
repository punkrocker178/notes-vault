### Add remote
`git remote add origin https://github.com/user/repo.git`

### Save git credential
`git config --global credential.helper store`

### Enable this to separate git credentials for different repos
`git config --global credential.github.com.useHttpPath true`

### Delete branch local (multiple delete):
`git branch -d $(git branch | grep -E ‘<branch-name>’)`

### Delete branch remote:
`git push -d origin <branch_name>`

### Delete multiple branch using regex, grep is used for filter output with regex, sed then use that ouput to edit(omit “origin/”)
`git push -d origin $(git branch -r | grep -E '<regex>' | sed -e 's/origin\///')`