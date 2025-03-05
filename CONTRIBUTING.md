# I. prerequisites

* git client
* any text editor
* optional: [jedrasiak:research:desktop](https://github.com/lukaszjedrasiak/research-desktop)

# II. workflow

## 1. fork the repository

First, fork the `lukaszjedrasiak/graph-ai` repository on GitHub

## 2. clone the fork locally

```
# Replace <your-github-username> with your GitHub username
git clone https://github.com/<your-github-username>/graph-ai.git
cd graph
```

## 3. add upstream repository

This allows you to sync with the latest changes from the main repository.

```
git remote add upstream https://github.com/lukaszjedrasiak/graph-ai.git
git fetch upstream
```

## 4. create and switch to the private branch

The private branch should be created from your main branch, which is a copy of the repository's main branch.

The `private` branch serves as a workspace for changes before selectively pushing to main. This allows contributors to keep some work unpublished while controlling what gets merged.

```
git checkout -b private main
```

## 5. make changes in private branch

Edit files, add new features, or fix bugs. Once changes are made, commit them:

```
git add .
git commit -m "Description of changes"
```

## 6. selectively move changes to main branch

Keep your `private` branch private and publish only selected changes.

```
git checkout main
# Replace 'foldername' with the modified folder or file
git checkout private -- foldername
```

This command brings only the specified file or folder from `private` into `main`, without affecting other changes in `private`.

When commiting under `main` branch follow the rules of conventional commits described below.

## 7. push changes to your fork

Ensure `main` branch is updated in your fork. If you want to keep your private branch local and unpublished, you can skip pushing it.

```
git checkout main
git push origin main
```

## 8. create a pull request

Go to your fork on GitHub.

Open a pull request from your main branch to `lukaszjedrasiak/graph-ai` main branch.

## 9. repo owner reviews and merges changes

The repo owner reviews and rebases the PR before merging.

## 10. sync your fork with upstream

To keep your fork updated:
```
git checkout main
git fetch upstream
git rebase upstream/main
git push origin main

git checkout private
git rebase main
```

If conflicts occur during rebase
```
git status  # See conflicting files
git mergetool  # (optional) Use a merge tool
git add .  # Mark conflicts as resolved
git rebase --continue
```

## troubleshooting

* "My branch is outdated." -> `git fetch upstream && git rebase upstream/main`
* "I accidentally committed to main." -> git reset HEAD~1
* "My PR has unrelated commits." -> git rebase -i upstream/main (interactive rebase)

# III. conventional commits

General rules:
* one note -> one commit -> one pull-request
* try to not change yaml properties starting with underscore (_)

## structure of message

```
<type>[optional scope]: <description>
[optional body]
[optional footer(s)]
```

## types

* `add` - new vertex
* `update` - changes in existing vertex
* `rename` - change of the vertex name
* `delete` - remove note
* `typo` - fix typo

## scopes

* `docs` - any changes in project documentation (e.g. CONTRIBUTING.md, LICENSE.md, README.md)
* `git` - changes related to git configuration (e.g. .gitignore)
* `.research` - changes related to graph settings

## examples

* `rename: old-name -> new-name`
* `add: new-note`
* `update: changed-note`
* `update(docs): change CONTRIBUTING.md`