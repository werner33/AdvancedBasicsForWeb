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
