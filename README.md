# learn-interactive-rebase

An interactive tutorial to gain interactive rebase skills!

Recommended prequisites:

- VSCode or your preferred text editor

## Preparation

Unless you love working with a command line text editor like vim, consider updating your git config to use your visual text editor for interactive rebasing (VSCode has a great interface):

```bash
git config --global core.editor "code --wait"
git config --global core.visual "code --wait"
```

## Let's Go!

1. Clone this repo and create your working branch locally

   ```bash
   git clone git@github.com:louisebolden/learn-interactive-rebase.git
   cd learn-interactive-rebase

   git checkout -b your-initials/branch-name
   ```

2. Create a subdirectory that contains a file of code that represents your work, then create a commit for it

   ```bash
   mkdir my_subdir
   touch my_subdir/my_work.rb # and add some code to this file

   git add .
   git commit -m 'My work is all done'
   ```

3. Wait! You've been asked to add something - extend your code with something new and create an additional commit for it
4. Now let's experiment with a commit that we might want to get rid of later:

   ```bash
   touch my_subdir/extra_file.rb # and add some code to this file

   git add .
   git commit -m 'Not sure this is needed'
   ```

5. Now you've run a linting tool and been told to make some tiny changes - go ahead and do this, then:
   ```bash
   git add -p
   git commit -m 'Linting fixes'
   ```
6. OK seems good - time to push your commits to a remote branch and open a PR
7. After opening a PR, view the list of commits - we can tidy these!
8. Back in your local branch:

   ```bash
   git checkout -b your-initials/branch-name-2 # duplicate your working branch so you don't need to worry about losing any of your work
   git push # push this copy up to the remote repository so it's safe

   git checkout - # return to the original version of your working branch
   git rebase -i main # let's go!
   ```

9. During the rebase process, you can select to:
   1. `drop` the "Not sure this is needed" commit
   2. `fixup` the "Linting fixes" commit
   3. `reword` the "My work is all done" commit (provide a clear explanation to help your teammates review)
10. When you've finished rebasing your branch, use `git log` to check the changes you've made to the commits in your branch, and then `git push -f` to overwrite your remote branch with your local branch's commits
11. Now if you refresh your PR, you should see the tidy and helpful commits. You can step through them as a final self-review before you ask your teammates to review

### Bonus

Once someone has merged their PR into the main branch on the remote repository, everyone else can run `git fetch` and `git rebase origin/main` in their working branches to bring the latest commits from main into their branch. The commits from their branch are 'replayed' on top of the new commits from main. This is much tidier than using `git merge`, as it avoids creating an unnecessary merge commit.
