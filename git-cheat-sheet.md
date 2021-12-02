# Introduction

Day2Day stuff related to git.

## Error-cases

### fatal: No annotated tags can describe

Due to the commit reference not found on describe in any tags (weird)

```
# fails:
git describe
# fix:
git tag -a "annotated-tag" -m "fix error-fetching"
# test:
git describe
```

## Commands

### Rebase

```
git rebase -i HEAD~<num-how-far-back-to-rebase-to?>
git commit --amend
git push --force origin <branch>
```

### Uncategorized

```
# Fetches all changes from the remote - also removes branches/tags that has been removed
git fetch --all --prune

# HARD-DELETE UNPUBLISHED COMMITS
# This will destroy any local modifications.
# Don't do it if you have uncommitted work you want to keep.
git reset --hard 0d1d7fc32

# Alternatively, if there's work to keep:
git stash
git reset --hard 0d1d7fc32
git stash pop

#### UNDO PUBLISHED COMMITS
# This will create three separate revert commits:
git revert 0766c053 25eee4ca a867b4af

# It also takes ranges. This will revert the last two commits:
git revert HEAD~2..HEAD


# Reverting a merge commit
git revert -m 1 <merge_commit_sha>

# To get just one, you could use `rebase -i` to squash them afterwards
# Or, you could do it manually (be sure to do this at top level of the repo)
# get your index and work tree into the desired state, without changing HEAD:
git checkout 0d1d7fc32 .
git commit

# Accept other people changes into your branch, regardless of what you've done.
git pull -s recursive -X theirs


# Configurations
## Disable https-verification for repo
git config http.sslVerify "false"
## ..or globally.
git config global http.sslVerify "false"

# Logging
## See all changed stuff within one or more commits:
  git log --numstat
  git log --shortstat

# Re-initialize with new updated .gitignore-file
## This will remove and add all files to your local cache. Note: This will also generate a rather large "touch". Be aware :)
git rm -r --cached . 
git add . 
git commit -m ".gitignore reinitialized"

# Remove all untracked files

## Print all untracked files
git clean -f -n
## Clear all untracked files
git clean -f
```
