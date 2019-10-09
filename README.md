# git-guidelines
A condensed guide for how to painlessly use git with the squash and merge strategy.
Please note that this guide was written for a course that used Azure DevOps. What this means is that all references to "Tasks"
would be Issues in Github language.

And lastly, nothing is never really finished is it? If you have questions or opinions, please get in touch by opening an Issue.
Thanks.



# Git rules! :metal:

In order for everyone to have a smooth development experience we need to establish some guidelines. Please read through this at least once, hopefully you will enjoy this condensed guide through out this course.

# Initial setup
Before you do **any** work, you should complete this guide. 

## Set up SSH in git and Azure DevOps
Generate an SSH-key according to this [guide](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key) if you don't already have one configured in your git client. 
When you have completed the previous step you should copy the contents of your `id\_rsa.pub` key into the web interface of Azure DevOps. Navigate to your profile, click on security, under the security tab you find the SSH public keys section where you can click add and paste your key contents. 

> :warning: When making your initial clone of the repo, make sure to clone the repo using SSH.

## Pushing large files
When wanting to push large files to the repository, such a s pictures, binary blobs, ISO's or whatever you may desire we need a separate tool. The reason beeing is that the history and size of the repository will quickly grow big and get slow at fetching and pulling. Git will count a change of a binary files as a complete file change and thus making the repo big quickly. 
### Git-lfs to the rescue!
In order to manage large files by git without slowing down the repo we install git-lfs. Refer to the [git-lfs](https://git-lfs.github.com/) website to install a version that works for your OS.
### Adding another filetype to Git-lfs
To track a new type of file not already tracked in the project, you use the command ```git lfs track *.bin``` where you change `.bin` to the filetype you want. The star symbol makes the command track ALL files that end with `.bin` in the repo


# Workflow
The workflow is simple, just follow these few steps and you will be all set.
Summarised workflow is as follows.
- [x] git pull
- [x] do work in your branch
- [x] git push to your remote branch (often).
- [x] create PR if none existent
- [x] finish work, merge master into your branch.
- [x] when approved, merge code into master.

There is many ways you can handle merges but we opt for the "squash-merge". If you are interested in why, you can take a look [here](https://blog.dnsimple.com/2019/01/two-years-of-squash-merge/).

--- 
   
![gitflow](https://i.ibb.co/9NVcsXB/git-flow2.png)


## Before starting to code you should
Go into Azure DevOps and make yourself the asignee of the **Task** of the **User Story**. Good, now everyone in the team knows that just *you* are working on this and we won't have several people working on the same thing by mistake.

### First, git pull!
First, you should always issue a `git pull` in your project repository before you  start a coding session.
If everyone uses the latest code when developing we will drastically reduce the amount of turbulent merges in the repo.  If you need to base your work on features that are not yet merged into master but available in a feature-branch, still issue git pull before each developing session inorder to keep up with the remote branch. Whilst this is ok, we recomend contacting the Git-master regarding any insecurities that may arise.
 
### Create a branch for your **Task**
Good, you have completed all the preliminaries and are soon ready to write code (yay!). If any of your team members also assigned to the same **Task**, has already created a local branch for the **Task**, they should now push this to make it available to the rest of the team members to pull this branch. Now, you should issue the command  ```git checkout -b "my-feature"```, which creates a new local branch with the name "my-feature". The branch name should be named something that relates to the **Task** that you have assigned yourself to above. If you instead pulled a branch that your team members created you can switch to it by issueing ```git checkout "name-of-branch"```. You are now ready to commence programming!

### Tracking progress of a **Task**
In order for other people in your team to be able to contribute or track progress of a evolving **Task**, we need to push often. Since each feature or bugfix is in it's respective branch we can achieve good parallellism without disrupting the development of other **Tasks**. Frequent pushes also makes life easier for your friends that will review your pull request in the end. This is due to the fact that it's easier to grasp 50 lines than 500. In addition, reviewers can catch critical design flaws earlier, which might result in you only scrapping 50 lines of code instead of 500 thus saving time in the end.

In order for easier tracking it's good if you make your Pull Request right after your first push to the current branch you're working on. With this done, you also request review from the two people that will review your work. One should be within your team and the other one should be part of some other team. Don't just assign an arbitrary person, ask them first to avoid skewed workload and angry faces. :)

### Reviewing code
When reviewing some ones code you are supposed to read through the committed lines and the meaning of them. Check so that the variable names are sensible and that the formatting is nice (or maybe follow a future code guideline). Also check so that the commit under review does not contain any out commented code. Check so that the code written has comments at advanced or unclear paragraphs. Remember to be clear in your feedback without being rude, you might just have misunderstood. 
In order to lighten up the reviews we enforce the use of GIF's.  
![](https://media.giphy.com/media/cFkiFMDg3iFoI/giphy.gif)   
You can insert these directly in to a comment by writing 
```
![some text](https://link.to.gif)
```


### Finishing a **Task**
Okay, so your code is working and the two reviewers are happy with everything from code style to variable names, nice! If you have built something that integrates with existing code you will need to merge it. This is done easiest by issueing ```git pull origin master``` while in the feature branch. If nothing clashes, git will just prompt you to write a commit message for the merge, this is usually pre filled with quite a self explanatory message that does suffice withot further comments. However, if your changes clashes with the master branch, you will be greeted with a list of files where manual picking of code snippets are needed. If you're unsure of what to do here, consult the git master. 

The only thing left to do now is receive a new approval from the reveiwers, wait for our CI tests to come back all green and then press merge in the web interface!

Congrats on your first contribution to the project!:beers:
