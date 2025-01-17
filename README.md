# COLLABORATIVE GIT FLOW

There are many aspects of group work. This lesson will focus specifically  on using git and gitHub as a collaborative tool.

> <br>Git - Open source version-control system <br>GitHub - Platform for hosting and collaborating on Git repositories <br><br>*Definitions from [GitHub Cheatsheet](https://training.github.com/downloads/github-git-cheat-sheet.pdf "GitHub Cheatsheet")*

Git is the program that is used locally in your terminal for version control. In order to achieve this it uses `branches` and a process called `merging`.  GitHub mirrors a lot of the functionality of git, it also has the ability to branch and merge.  I think of git being a tool on my local machine used for version control and gitHub being like facebook for my code.  

<br>

Here is the basic flow we will be establishing:

![Git Flow Diagram](./images/gitFlow.png)

<br>

## GET ORGANIZED

A little planning goes a long way!  Before initializing a repo or writing any code it is beneficial to come together as a group and establish a few things:

- Determine who likes to work on which aspects of the code.  Some of us are more front end oriented some are more back end.  One of the benefits of working in a group is leaning on each others' skills AND learning from each other.  Each person in the group should have a high level understanding of what each member is doing with their code even though they may not be working on that specific part.

- Agree upon a basic file structure.  As we code more and more projects we may find ourselves repeating a lot of the same tasks or setup.  This is another thing to lean into.  From the culinary world there is an idea called *mise en place* which essentially means *putting everything in it's place*.  When we are consistent about how we set things up from project to project it will help us build muscle memory and allow us to focus on the project itself.  The opposite of this may bee seen as re-inventing the wheel each time  

- Having a layout for the file structure beforehand will help us avoid merge conflicts down the road.

- Determine who will initialize the repo.  While each person will eventually be a collaborator, one group member will set up the initial repo and then make others collaborators.  Each team member will clone the project to their local machine.

<br>

## SET UP THE REPO

One person in the group should take care of this part

<br>

### INITIALIZE 

Navigate to your gitHub account online.  In the top right hand corner there is a `+` button.  This will open a drop down menu, select new repository.

![New Repo Init](./images/newRepo.png)

<br>

Fill out the form to create a new repo:
- Name
- Description of the repo (optional but recommended)
- Add README (for sure!)
- Add .gitignore based on your project template (if available)

Click the green `Create repository` button

<br>

### INVITE COLLABORATORS

1. Open the settings page by clicking `Settings` tab.  
2. Click on the first submenu under `Access` which is `Collaborators`.  
3. Within this page there is an `Add people` button.  Use this to invite your group members


![Add Collaborators](./images/addCollabs.png)

Find your team mates using their gitHub handles or email addresses.  Select each person and click the green button to send them an invite.

![Invite Modal](./images/Invite.png)

<br>

This will send and invite to each of the group member's email addresses as well as their gitHub account.  As a collaborator make sure you accept the invite or the owner of the repo will see something like this, until you do.

![Invite Modal](./images/pendingInvite.png)

<br>

### CLONE

At this point only the person setting up should clone the repo in order to set up the dev branch.  

In the terminal clone down the repo to your local machine:

*note: the address below is for the `collaborativeGitFLow` repo.  Your group's address will be different*

```
git clone git@github.com:IntuitiveHarmony/collaborativeGitFlow.git
```

<br>

### CREATE A DEV BRANCH

This is the "staging" branch to test out new features on.  This will be a copy of the main branch and it is where we will pull in our code from feature branches to make sure it merges properly with what we already have on the main branch and what other people have been working on inside their feature branches.  

Run this command in the terminal:

```
git checkout -b dev
```

The `checkout` command allows us to switch between branches.  The `-b dev` creates a new branch called `dev`, makes a copy of the branch you are on and  switches to `dev`.

In order to see the all the branches in a repo run in the terminal:

```
git branch
```

The asterisk tells us which branch we are currently on.  If you have oh my zish installed you may have another sort indicator of the current branch, notice the `dev` in pink on the command line.  This is useful to visually not only see which branch you are on, but that you are in a git repo.  

![Terminal branches](./images/terminalBranch.png)

<br>

Once this branch has been made locally, push it to gitHub.  In the terminal run:

```
git push origin dev
```

This will push the `dev` branch to gitHub.  Navigate to gitHub, REFRESH the page and you should see the new branch in the dropdown menu on the left side of the page.

![Dropdown of Branches](./images/devBranch.png)

<br>

### ADD BRANCH PROTECTIONS

This step is not necessary, but it is highly recommended in order to protect all your group's hard work.  This is a way to add another layer of protection for your valuable main branch. Essentially we are going to make it so any one of the collaborators cannot just edit the code on the main (or any other protected) branch 

Back in the: 
1. Settings page 
2. Navigate to the `branches` sub menu under `Code and automation`
3. Click the `Add branch protection rule` button

![Add Protection Rules](./images/protectionFlow.png)

<br>

This is the page where we can add rules to help protect our branches.  The ones that we are going to implement is `Require a pull request before merging` clicking this will open another menu. `Require approvals` should already be checked.  We can increase the number of approvals if we want but one should be enough for our purposes.  

Towards the end of the page select the radio buttons labeled `Lock branch` and `Do not allow bypassing the above settings`.  

Do this for both the `main` and `dev` branch. 

![Rules Dropdown](./images/branchProtection.png)

...

![Rules Dropdown](./images/bypassBranch.png)

<br>

Essentially the `Require approvals` puts a restriction within gitHub that requires someone from your team to review code before it is merged with any protected branch. (*i.e. `git push origin main` no longer works*)

The `Do not allow bypassing` make the rules we just put in place to apply to everyone collaborating on the repo.

If anyone try's to push to `main` or `dev` they will get the following error: (more on this later)

![Review Error](./images/reviewError.png)


When this is complete we should have something that looks like this:

![Protection Rules Home](./images/protectionRulesHome.png)

<br>
<hr>

## COLLABORATORS CLONE REPO

At this point the rest of the group members can clone down a copy of the repo to their local machines. So that everyone can start on their pre-decided tasks. 

*note: the address below is for the `collaborativeGitFLow` repo.  Your group's address will be different*

```
git clone git@github.com:IntuitiveHarmony/collaborativeGitFlow.git
```

Remember to work off a branch for each new feature. *note: branch names should be unique from eachother*

While in the main branch in the terminal run:

```
git checkout -b newFeature 
```

Commit as you normally would while working within your new branch.  Once you are satisfied that the work is complete and your feature is working push your work up to gitHub on your `newFeature` branch.  After that it is time to do a `pull request`.

<br>

## MOVING A COMMIT TO ANOTHER BRANCH

Remember this error?

![Review Error](./images/reviewError.png)

<br>

Lets say we accidentally committed work locally on a protected branch.  We won't be able to push it, what now?  If you have started working on a protected branch still add and commit.  moving the commit is fairly simple.  

First we need to make the branch we want to move or commit to.  Once all your work is committed in the terminal run:

```
git checkout -b <new-brach-to-move-my-work>
```

This will create a new branch with your commit in there.  Go ahead and push this to gitHub if you want or simply continue to work from here. 

We still need to reset the `HEAD` or top commit in the protected branch.  If we checkout `main` and run `git status` We can see that it is ahead by one commit, this is the commit we just moved to our new branch.  

![Branch Ahead](./images/branchAhead.png)

<br>

To find the list off previous commits in the terminal run:

```
git log
```

You should see a list something like this print in your terminal. 

```
commit 4b75f52916bfa40747d5bb34e15d986c1ba97776
Author: Intuitive Harmony <j.horst77@gmail.com>
Date:   Wed Mar 8 08:50:06 2023 -0700

    commit to move

commit a456b041a3ed4d95f485877e7d76a04b4b031bb9
Merge: 006d01f 4b75f52
Author: IntuitiveHarmony <j.horst77@gmail.com>
Date:   Wed Mar 8 08:47:45 2023 -0700

    Merge pull request #23 from IntuitiveHarmony/image
    
    aqua back

```

Find the commit before the one you made and copy the long string of numbers and letters, since it is on a protected branch the commit will more than likely be a merge.

In the terminal run:

```
git reset --hard <commit-before-the-commit-you-moved>
```

This is what it looked like in my case.  

![Head Reset](./images/headReset.png)

<br>

You should see the following in the terminal and now be back on track.  Just make sure to checkout the feature branch you are working on!

![Clean Branch](./images/branchClean.png)

<br>
<br>

## PULL REQUESTS

Usually when someone pushes their code to gitHub there will (usually) be a message saying so and a button `Compare & pull request`  If this button is not there and you are sure that you pushed the code to gitHub.  You can create a new pull request in the `pull request` tab. Both options take you to the same screen.

![Pull Request](./images/pullREquest.png)

<br>

Once you press the `Compare and pull request` button it will take you to an other screen that needs a little attention. 

1. Since `dev` is our staging branch before the `main` branch we need to switch the base to `dev`.  Use the drop down menu on the left.  Make sure the compare branch is set to the `newFeature` branch
2. You can request a review from someone in your group but it is not necessary.  At the beginning it is beneficial to complete pull requests together anyway.  That way the author can speak to the code if need be
3. Press the green `Create pull request` button

![Compare Changes](./images/compareChanges.png)

<br>

Once this is done it will take us to a screen that shows us what is going on the the pull request.  People can check any changes, make comments on the code and provide a review.  You can see that the red warning labels are requiring a code review before merging.  This was because we set the branch protections earlier.

![Review Required](./images/reviewRequired.png)

<br> 

### CODE REVIEW AND APPROVAL

Since we set up our branch protections we will have to wait for one of our team members to review and approve our code before it can be merged.  Again, we se this up in order to protect or code with some check and balances.  It would be good practice to send a message to your team saying that you pushed your new feature.


In order to complete the code review click the `Files changed` tab.  This window will show all of the changes that took place within the last commit of that branch. Click on the review changes button.  You can approve or request changes.  If you approve you will be able to merge the code in the next step.  If you request changes the other user will have to update the code and push those changes before approval by your peers. 

![Files changed](./images/filesChanged.png)

![Fire Review](./images/fireReview.png)

<br>

You can also use the blue `+` sign to highlight certain blocks of code to comment on and start a review. You will still have to finish the review using the method described above.

![Review Method 2](./images/anotherREviewMethod.png)

<br>

Then submit the review.  If it is has been approved then you move on to the green `Merge pull request` button.  The last step is to confirm the merge by pressing the `Confirm merge` button on the next page (I always forget this). Once you complete all this, the `newFeature` branch is now merged with the `dev` branch.   

Just make sure you see the purple at the end to ensure you have completed the process.

![Pull Success](./images/pullSuccess.png)

<br>

### GIT PULL ORIGIN DEV

Collaborators can now go to the `dev` branch and test out the new feature.  Save and commit any changes you have on a branch you may be working on and checkout the `dev` branch.
*Make sure you are on the `dev` branch before pulling!*

```
git checkout dev

git pull origin dev
```


Use this as a testing ground to run the code with the code from the two branches merged, make sure the code all works together and all your previous functionality is maintained.  If other collaborators have branches to merge it is best to do individual pull requests to the `dev` branch and test them one at a time so bug hunts are minimal. 

Once everyone is satisfied that all of the new features are working properly, create a new pull request in gitHub from the `Pull requests` tab. This time set the base be the `main` branch and set the compare to `dev`. Follow the above steps to complete a pull request.  Once this is done collaborators are able to work on their next tasks.  

<br>

## MERGE CONFLICTS 💀

Duirng the course of any project communication is essential.  If multiple people in a group try and make edits to the same file and then merge those changes it will trigger a merge conflict. This WILL happen.  This is why we have the `dev` branch, to hash out merge conflicts and bugs while our main branch is still protected. 

Let me repeat, if you work in a group project you will experience a merge conflict at some point.  They can range from a simple fix to nightmare catastrophe.  This is why it is important to know how to deal with them.  We can provide a simple example. 

*In order to focus on merge conflicts themselves the following example won't involve any code.* 

Let's look at how gitHub responds when we try an merge a file that has been edited by two different collaborators.

In this repo we have an `index.html` and `main.css` file.  Let's make a scenario where two people update the `main.css` and then try and merge them. 

One of our collaborators had a `greenBackground` branch and another had a `redBackground` branch, they both made changes to the original background color in the css file.    

Whichever one pulls down to the `dev` branch shouldn't have any conflicts.  It is when we pull the other one in to the `dev` branch that the conflicts will become more apparent.  In this case I pulled the `redBackground` branch into `dev` first. and it merged just fine. Once we try and merge the `greenBackground` branch this error comes up:

![Merge conflict](./images/greenToMain.png)

<br>

Press the green `Create pull request`.  This will take you to a screen where you can resolve the merge conflict.  For more complicated merge conflicts gitHub may ask you to resolve them in your text editor.  Follow the prompts they provide in this case.

Either way you are going to see something like the following code block.  It is showing you that the css in `greenBackground` is darkseagreen and that it is dark red in the `dev` branch, remember, we already merged the `redBackround` branch to `dev`

```
body {
<<<<<<< greenBackground
    background-color: darkseagreen;
=======
    background-color: darkred;
>>>>>>> dev
}
```

Whether you are in gitHub or your text editor you will decide which block of code to keep by deleting the code you don't want and the lines with `<<<<<<` `=======` and `>>>>>>`. You can also change the background color to something different entirely.  This is why having collaborators available for pull requests is beneficial. Once this is done click the `Mark as resolved` button to complete the merge to the `dev` branch.  moving forward it is best to delete (or not work out of) any branches that contributed to a merge conflict because it will keep coming back up!


## HUNGRY FOR MORE

The best way to learn these tools is to use them!  I reccomend finding a partner (or two) and work on setting up a mock repo using this markdown as a guide.  Work with simple code or README files and make branches, protect some of them, move commits to other branches, reset the HEAD, perform pull requests and merges even give yourself a merge conflict or two.  Better to practice now on a mock repo than on a big improtant project!