# GitHub Workshop
The recoding for the live session is available [here](https://datasciencewithdaniel.com.au/videos/DSWD-GitHub-Workshop-Recording.mp4).
# 1.0 Set-Up
## 1.1 Create GitHub Repository
Create an account on GitHub and create a new Repository under your account (or whoever you want to own the account).
## 1.2 Check Local Git Installation
Check to see whether you have Git installed on your system, if you do not, download it from [here](https://git-scm.com/).
```
$ git --version
```
## 1.3 Clone Repo to your Local Machine
Copy the HTTPS link to your GitHub Repository and clone it to your local machine. You may be prompted here to add GitHub credentials if you have not used Git/GitHub before - add the ones that you use for your GitHub account.
```
$ git clone https://github.com/datasciencewithdaniel/GitHub-Workshop.git
```
# 2.0 Branch Management
## 2.1 Check your branch
Always check what branch you are on before you start work to ensure that your work ends up in the right place. This is also shown in the bottom-left corner on VS Code.
```
$ git branch
```
You can add the ```-va``` option to the command to see the latest commit code as well as what message that commit had - this makes it easy to see which branch is at which commit.
```
$ git branch -va
```
## 2.2 Ensure you are working on the latest version
When working collaboratively, other people are going to be committing code to the Repository. This makes it a good practice to regularly pull down the latest version of the code. This is essential before merging any of your development changes into the ```main``` branch.
```
$ git fetch
$ git pull origin <my-branch>
```
Ensure that you are on the branch you want to pull the remote changes into before running the ```pull``` command as they go into your current branch.
# 3.0 Making Changes
## 3.1 Creating a New Branch
Now that we know how to manage branches, we have to see how to actually create them. This command is a combination of two other commands that first creates a new branch and then performs a ```checkout``` - which means you switch to being on the new branch.
```
$ git checkout -b <my-branch>
```
You can also simply checkout a branch which allows you to switch between branches depending on what work you want to do.
```
$ git checkout <my-branch>
```
## 3.2 Staging Changes
Once you have made changes to any files, you need to tell Git that these changes are there. Git does not know about new files that you have made so these are untracked the first time you create the file, and changes will be unstaged if you edit an existing file that is being tracked. You can check the status of your files to see where everything is easily.
```
$ git status
```
The following stages a file ready to be commited, and the second command stages all files in the local Repository.
```
$ git add <file>
$ git add .
```
## 3.3 Committing Changes
Once changes have been staged, you need to commit them to the branch you are working on. This essentially tells Git that these changes are 'locked in' and are added to the branch logs. Each commit has to have a commit message which should describe what is being committed. It is better to commit more often with smaller changes than one massive commit with everything as this allows for eaasier retracing in case anything does break.
```
$ git commit -m "<commit message>"
```
# 4.0 Merging Code
## 4.1 Merge Main into Development
Once you have commited any number of changes, these are only available locally on the branch that you commited the changes too. Best practice is to merge these changes locally and address any merge conflicts (where there are two different changes of the code that are not compatible). To do this, first bring the local ```main``` branch up to the same point as the remote ```main``` branch.
```
$ git checkout main
$ git fetch
$ git pull origin main
```
With the local ```main``` updated, change back to your branch that holds the changes and merge them together. This is where you need to address any merge conflicts. If there are none, the merge should happen successfully.
```
$ git checkout <my-branch>
$ git merge <main branch>
```
## 4.2 Push to GitHub
Your local branch has the changes that you want to incorporate, but only you can see them. The next step is to push them to the remote Repository so that they are visible to everyone else (but they are still on \<my-branch\>).
```
$ git push origin <my-branch>
```
## 4.3 Pull Requests
With all of the changes reflected in the remote Repository, you raise a Pull Request (using the buttons) to merge the changes from \<my-branch\> into the ```main``` branch. This request summarises all of the changes that are being added and where, and is the location where a review often occurs. Often a discussion is had in the Pull Request as the person making the changes summarises what they have done and the reviewers ensure that this is not going to break anything. 

Pull Requests can be changed/added to if required to ensure that once approved and the merge occurs, everything is working smoothly. Once the Pull Request is complete, the cycle begins again, using the following to update your local main branch.
```
$ git fetch
$ git checkout main
$ git pull origin main
```
## 4.4 Deleting Branches
Once you have completed a feature you often want to remove the branch to only have branches that are being actively developed. The first command removes a local branch and the second removes a remote branch. Be careful here to not remove the remote ```main``` branch!
```
$ git branch -d <my-branch>
$ git push origin --delete <my-branch>
```
# 5.0 Git Tips
- VS Code colour changes files depending on Git and Git extensions in the marketplace can make it easy to see where changes have been made and by who.
- Running ```git log``` will allow you to look back through the commits on your branch.
- A good Git guide can be found [here](https://nvie.com/posts/a-successful-git-branching-model/)
# 6.0 Virtual Environments
There are multiple ways to have a Python virtual environment, one of the best is through the use of Conda which we will explore, however you can use packages that come with Python such as ```virtualenv```, which has a guide [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/).

Virtual environments allow all of your Python packages to be installed in an isolated place, allowing you to have specific control over which packages and which versions your code is accessing, and running multiple environments allows for different versions of the same package to be on your system for different uses.
## 6.1 Conda
Conda is a package manager that forms part of the Anaconda distribution (which you may already have), otherwise it can be downloaded from [here](https://docs.conda.io/en/latest/miniconda.html) as miniconda. You can verify your Conda installation the same as we did for Git.
```
$ conda --version
```
Conda can show you all of your virtual environments easily as it creates and stores them in a centralised location (which is different to ```virtualenv```).
```
$ conda info --envs
```
## 6.2 Creating an Envionment
With Conda ready to go, all we have to do is create our virtual environment. You can simply create it, or specify some of the settings such as which Python version you want to use inside. All creations will promote you with a [y/n] to proceed.
```
$ conda create --name <my-env>
$ conda create -n <my-env> python=3.9
```
## 6.3 Activating an Environment
Once you have an environment created, you can simply acitvate it from anywhere on your system. Once you activate it, you can see your current environment in the terminal.
```
$ conda activate <my-env>
```
Once an environment is activated you can use Conda (or Pip) to install the packages you would like, and you can specify a version if what you want is not the latest.
```
$ conda install -n <my-env> scipy
$ conda install -n <my-env> scipy=0.15.0
```
If this does not work, either use a different Conda [channel](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html), or use Pip.
## 6.4 Deactivating an Environment
Conda envrionments can be easily deactivated once you are finished using it.
```
$ conda deactivate
```
## 6.5 Conda Tips
Often you want to see what is in your Conda environment, and the following lists all of the packages curently installed.
```
$ conda list
```
If you want to ensure that you (or another teammate) is working off the same environment, you can build a environment.yml file that contains details of your current packages.
```
$ conda env export > environment.yml
```
This can be then used when creating a new Conda environment.
```
$ conda env create -f environment.yml --name <my-env>
```
You can also remote environments you no longer require.
```
$ conda remove --name <my-env> --all
```
# 7.0 Other Tips
- Pre-commit is a Python package that you can use to run checks before your commit is processed. This can ensure consistent formatting and style. Check out a simple style/formatting pre-commit [here](https://github.com/datasciencewithdaniel/GitHub-Workshop/blob/main/.pre-commit-config.yaml)
- .gitignore is a file that specifies files that you don't want Git to track at all, often this includes system generated or user-specific files that are generated. Check out an example file [here](https://github.com/datasciencewithdaniel/GitHub-Workshop/blob/main/.gitignore)
- Ensure that your Repository has a README file (which this file is) that explains what is going on in your Repo and points people to any files they should be aware of.
- You can add [badges](https://shields.io) to public Repositories (and some to private Repositories) that can provide insights into the Repo.
