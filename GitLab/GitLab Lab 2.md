GitLab Lab 2

# LAB 2: WORKING WITH GIT LOCALLY
## Verify git is installed locally

Open a terminal session or command prompt and type git version. If it prints a version number, git is installed.
## Generate an SSH key

These steps are only needed if you do not have an SSH key already installed.

 1. In a terminal or command prompt, type `ssh-keygen`
2.  If prompted for a key type, choose `ed25519`, which is more secure than the more older `id_rsa` type.
3.  You will be prompted to select the location in which your key will be saved. Press **Enter** to leave it at the default.
4.  You may be prompted to create a passphrase. Leave it blank or enter a passphrase of your choice, and then hit **Enter**. If you do use a passphrase, you'll have to enter it every time you push or pull code from GitLab.com.
## Add an SSH Key to Your GitLab profile

 1. In the top right-hand corner of the the GitLab app, locate your user avatar and click the **down arrow**.
2.  From the dropdown menu, click the **Edit profile** item.
3.  On the left-hand side of the screen, click on **SSH Keys**.
4.  If you have no SSH keys added to your profile, you will land on the **Add an SSH Key** screen.
5.  Return to your terminal/command session. To retrieve the SSH key you created, move into the folder you saved it to by typing `cd {file path}`
6.  Type `ls -al` to see two key files: a public key and a private key. The public key is called either `id_ed25519.pub` or `id_rsa.pub` and is what you need to share with GitLab.
7.  Type `cat id_ed25519.pub` or `cat id_rsa.pub` (depending on which kind of key you generated) to print the contents of your public key. Copy those contents to your clipboard.
8.  Return to the GitLab app in your browser. Paste the public key contents into the `Key` field, enter any title you want in the `Title` field, and click **Add key**.
9.  Your local computer is now authenticated to push and pull (interact) with GitLab.
## Copy (clone) a project repo to your local machine

 1. Use the top navigation bar to get back to your **Project Overview** by clicking **Projects** > **Your projects**. Find your **Top Level Project** by looking for the one with the Owner label next to it (you might need to advance to the next page of projects).
2.  Locate the blue **Clone** button and click the dropdown arrow.
3.  In the **Clone with SSH** section, click the **Copy URL** button.

## Create a directory on your local machine

 
- **Note**: The following git commands are summarized in GitLab's helpful git cheat sheet.

 1. In your terminal/command window, type `cd` to get out of the `.ssh` directory and into your home directory.
2.  Type `mkdir` training to create a new directory.
3.  Type `cd` training to move into your new directory.
4.  Type `git clone <URL you copied previously>` to copy the git repository from your **Top Level Project** onto your local machine.
5.  Move into the repository you just cloned by typing `cd top-level-project`. This is where git will track your changes, and where you will interact with the repo and git.
6.  Type `ls -al` to see a list of all files in your current directory, including hidden files.
7.  Type `git status`. You will see a message saying your working tree is clean.

## Work on a branch

 1. Type `git checkout -b temporary_branch`
2.  Type `git branch -a` to see all branches.

**Note**: *the red branches are on the remote server* (GitLab.com).
## Make a change to a README file

 1. In your terminal/command window, navigate to the directory that contains the `README.md` file.
2.  Using the editor of your choice, add a new line `a second line added to master branch locally` at the end of `README.md`. Save the file.
      - **Developer Tip**: Visual Studio Code is the preferred editor of most GitLab users, but any text editor (including Sublime Text, Atom, or vi) will do.
4.  Type `git status` to see if git has noticed that the file has been modified.

**Note**: Git has detected that we have edited a file in our local repo, but since we have not created a "commit" yet, git has not yet added that edit to a snapshot.
## Add `README.md` to the local GitLab staging area

 1. Type `git add README.md`. If this is successful, git will produce no output. The `add` command doesn't move `README.md` on your filesystem, but it does add it to what git calls a "staging area".
2.  Type `git status` to see that `README.md` is now ready to be committed (that is, it has been successfully staged).

## Commit the changes to `README.md`


 1. Type `git commit -m "added a second line to readme.md"`
       - **Developer Tip**: You can stage and commit a change at the same time by using the `git commit -am "commit message"` command to save time!
3.  You have now created a record or point-in-time snapshot of the file that you can refer back to if needed.
4.  Type `git status` to see that the staging area is empty again, following the commit.

## Push Your changes to the **temporary_branch** on the remote GitLab server

 1. Type `git push -u origin temporary_branch`. Enter the passcode for your SSH key if prompted. This creates a new branch on the GitLab server called **temporary_branch** and pushes your changes to that branch.
      - **Developer Tip**: If you are ever unsure of the exact command to push your changes to the remote server, type `git push` and git will output an error message with the correct commands you can copy/paste.

## Modify your content again

 1. In your local machine's text editor (not the GitLab.com editor), add a new line to your local copy of `README.md` that says `add a third line to file`, and save the file.
2.  In your terminal/command window, type `git add README.md` to move the edited file to git's staging area.
3.  Type `git commit -m "modified README.md"` to commit the file that was in the staging area.
4.  Type `git log` to see a description of the commit you just made.
5.  Type `git push` to copy the edited `README.md` to the repo on GitLab.com.
    - **Developer Tip**: To commit your changes to the upstream branch (that is, the branch on the remote server with the same name as the branch on your local machine), simply type `git push`. The system only needs to set the upstream branch once.
6.  Navigate to your GitLab.com project in your browser, switch from **master** to **temporary_branch** using the dropdown under the project's title, and confirm that your local changes were pushed up.

## Simulate a change on the remote temporary_branch

In this section, let's simulate someone else in your organization making a change to the copy of **temporary_branch** that lives on GitLab.com. When we're done with this section, the remote and local versions of **temporary_branch** will be different: the code on that branch will have moved under your feet (so to speak)! In the section that follows this one, we'll see how to reconcile this difference.

 1. From the GitLab.com dashboard, navigate to the **Top Level Project** and click on **temporary_branch** from the dropdown just below the project's name.
2.  You are now looking at files in **temporary_branch**. Click on **README.md**.
3.  Click the **Web IDE** button.
4.  In the Web IDE screen, add a new line to the end of the file: `add a fourth line from the remote copy of temporary_branch`
5.  Click the **Commit**??? button.
6.  Check the radio button for **Commit to temporary_branch** and uncheck **Start a new merge request**.
7.  Click the **Commit** button to finalize the changes on the remote copy of **temporary_branch**. Since you made this change on the Gitlab.com server, the server's repository is now one commit ahead of your local repository.

## Refresh your local branch with `git fetch`

Since your local **temporary_branch** is out of sync with the remote **temporary_branch**, you must update your local copy of that branch to incorporate the changes from the remote copy.

The `git fetch` command retrieves the updated state of remote branches without updating the contents of your local branches. In other words, it tells you how many commits your local branches are behind the remote branches, but it won't make any changes to your local branches.

 1. Return to your terminal/command window and type `git fetch`. If you are prompted for your SSH passphrase, enter it.
2.  Type `git status` and review the updated status of your local branch.

## Pull from the remote (upstream) repository

You now need to explicitly tell git to update the contents of your local **temporary_branch** by merging in changes from the GitLab.com **temporary_branch**.

 1. In your terminal/command window, type `git pull` and check the output to see how many files it updated locally.
2.  Type `cat README.md` to view the updated contents of the file. You should see the fourth line that you added in the GitLab.com Web IDE.

## Merge all changes from **temporary_branch** into the **master** branch

 1. In your terminal/command window, type `git branch` to verify which branch you are currently working in. You should already be in **temporary_branch**.
2.  Switch to your **master** branch by typing `git checkout master`
3.  Type `git merge temporary_branch` to incorporate all changes from your local **temporary_branch** (in this case, just the modified `README.md`) into your local **master** branch.

## Update the remote repository

 1. In your terminal/command window, type `git status` to see that there are no changed files that you need to stage or commit and to confirm that you are on the **master** branch.
2.  Type `git push` to update the remote copy of **master** branch with any changes from your local copy.
3.  Navigate back to GitLab.com and view `README.md` in your project's **master** branch to view the changes.
