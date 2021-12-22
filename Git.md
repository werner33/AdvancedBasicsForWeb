# intermediate_git

Git is one of the most fundamental tools for managing collaboration when writing software. Although you surely have worked with Git since early on in your education at Pursuit. Git is a powerful and varied tool. There is always more to learn to manage workflow, increase harmony in collaboration and make sure that we don't lose important code. 

At a simple level, Git is a file that lives inside a software project that stores 'save points' as we go. We can jump to any save point at any time. Save points are generally called 'commits'. We'll start out by looking at a project and perusing the previous commits.

# git log 

Please fork and checkout [this repo](https://github.com/werner33/Sonnet).
 
One thing to note, is that we can just as well use Git to collaborate on an essay as on a website. This repo is a poem from William Shakespeare. Let's take a look at the commits that have been made until this point. We can do this by typing `git log` on the command line.
 
 Git log will reveal a scrollable list of all previous commits, including their time, date and author. When you are done looking at the commits, feel free to press `q` to exit the log. 
 
 The log keeps track of all committed changes, noting by whom and when they were committed. 

# git reflog 
 
As we work on an assignment, we may find ourselves sometimes thinking 'Where am I? How did I get here?' Or we realize we made a change that we really don't want to add to the codebase. For this we don't care so much about `git log` but rather `git reflog`. The reflog is a record of where we *personally* have been in a particular project. 

We haven't done much yet, but let's go head and check out the reflog. In the terminal type `git reflog`.
 
We don't have much to see here yet, but we'll see that this reflog grows as we work through the class. 
 
# Resolving a Git Conflict
 
 This next section may be a review, but it's important so I wanted to review it. 
 
 Generally when we take on assignment, we are working on a git `branch`. This allows us to do our own work without running into other changes that coworkers may be making. Often, your project managment software will automatically create branches, but if you need to create one from scratch, you can type `git branch <branchName>`. Let's do that now. 
 
 `git branch first-branch`
 
 We've created the branch but now we need to move to that branch:
 
 `git checkout first-branch`
 
 On the first line of the poem, go ahead and add a new line with whatever text you would like. Add this code and create a commit. 
 
 Now, while you are working on your branch, your coworkers are working on their own branches. Let's simulate that. First, let's go back to the master. `git checkout master`. Now, let's browse existing branches by typing `git branch`. We see that the astirik tells us that we are currently on `*master`. 
 
 Let's create a second branch: `git branch second-branch`. Note: we can create and checkout a branch at the same time by typing `git checkout -b second-branch'. Otherwise just move to that branch with `git checkout second-branch`.
 
 Since we never merged our `first-branch`, you'll see that the line that you added is not reflected on master or this new `second-branch`. Let's add a different first line on this `second-branch`. Type whatever you want. 
 
 Now, let's move back to master and we'll decide we're totally happy with the text we added. Let's merge it into master. 
 
 Type: `git merge second-branch`

 This should merge with no issues. However, we still have our `first-branch` hanging out with a different change in the same place. Before we merge `first-branch` lets delete `second-branch` since we're done with it now. To delete a branch type: `git branch -d second-branch`. Let's type `git branch` to confirm that we still have `master` and `first-branch` but `second-branch` is gone. 
 
 Finally, we want to merge the work from `first-branch`. Go ahead and type: `git merge first-branch`. 
 
 You will see something like this: 
 ```
Auto-merging test.js
CONFLICT (content): Merge conflict in test.js
Automatic merge failed; fix conflicts and then commit the result.
 ```
 
 Let's open this in VSCode and resolve the commit. Once we've chosen the change we want, we can type `get merge --continue` and complete the merge.
 
 
# Revisiting Reflog
 
 Now, that we've moved around quite a bit, let's look back at the reflog. We see we have many markers that we can revisit if we want to. Where as log only really tracks commits, reflog tracks commits as well as any time we merge, rebase, change branches and more. 
 
# Amend a Commit

Do you ever finish a ticket and think, "Finally, Done! Let me commit and push this real quick." And then, a few minutes go by and you think of one more small thing you need to add. Or that debugger you forgot to take out...

Amending a commit is a great way to make a small update to the code you just pushed - without creating a new commit. 

First, make any additional changes to your code. 

Then, type `git add .`, followed by `git commit --amend --no-edit`. When you include `--no-edit`, the commit message will not change. If you exclude that flag, you will get the chance to revise your commit message. This can be useful if your ammendment meaningfully changes the nature of your commit. 


# Squash Unnecessary Commits 

Sometimes you might be working on a particular task and you make several commits. However, when you look back at many commits, you feel that some of them are not useful and don't point to a place where you would ever want to go back to. As an example: 

first commit - "added a user profile page"
second commit - "laid out user image and summary"
third commit - "removed console.log"
fourth commit - "added a contact me section" 

One of these is not like the other... Let's see how we could use git to get rid of the third commit and 'squash' it into the fourth commit. 

Let's start with `git rebase i HEAD~4`. This will open an interactive rebase view in VIM. We can re-write the keyword beside the commit we don't want and change it to `squash`. This will squash it into the fourth commit. We could also potentially drop it - though that is a bit more risky since we are letting go of the code completely.  

# Interactive Rebase to Remove Old Code

We're going to end our journey through Git with an interactive rebase. Sometimes, you may look back and see that several commits ago, you included something in your code that has since been removed, but it't not enough to remove it from the active code. Rather, you need to remove it from the whole commit history. For this, we also use interactive rebase, but now, we want to use the `edit` keyword. Once we save this interactive rebase, it will essentially create a script that plays back each of our commits, allowing us to edit any of them we labeled with the `edit` key word. 

# More Resources

[Git for Four Year Olds](https://www.youtube.com/watch?v=1ffBJ4sVUb4&ab_channel=HackersOnBoard)
