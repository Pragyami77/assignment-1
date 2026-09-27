Git fundamentals

1. Git has three places a change can live: the working directory, the staging area, and the repository.
Describe each, and explain what you would lose if the staging area did not exist.

ANS : The working directory is a place where we create and edit the working project files.
The staging area contains the changes that needed to be committed later. 
The repository is a place where committed files and folder are stored and their history. It is generally called as repo.


2. git init and git clone both leave you with a Git repository. Explain what each one actually does, and give a situation where each is the right choice.

ANS : Both are essential part of the git.
git init helps us to create a new Git repository in an existing project folder. For instance, if I want to start a version control for my working project then I will use the git init.
git clone helps us to copy the existing remote repository to my computer, and they can be clone from the different GitHub sources, make our own changes in local computer.


3. What does a commit store, and why is "committing" not the same as "saving a file"? Why is Git much less useful if user.name and user.email are unset or wrong?  

ANS : A commit stores a snapshot of the changes that we have made so far along with the metadata or information such as author name, email, time and commit message. It also has unique hash that identifies the commit.
Commiting is different from saving a file because a "commiting" created a records the change in Git's database, making it part of the project's version history while "saving a file" updates the file on our local disk.
user.name and user.email are important as it helps to know who have made commit and changes in the project and without them team will find it hard to figure out who wrote that and why.


4. git status , git log , and git diff answer three different questions. State the question each one answers, and describe a moment in your workflow where you would reach for each.

ANS : 
git status shows which current state of working directory and staging are we are in. 
git log shows the history of previous commits.
git diff shows the changes between versions or between my working files and the staged /commited versions.
For example: checking status before we commit, checking log to find when a bug was introduced, checking diff before staging to review our own changes.


5. Explain what makes a commit message good. Why is "update" a genuine problem for a team six months later, and when is it worth writing a message body rather than just a summary line?

ANS : A good commit message briefly explains what was changed and why when necessary. 
A message such as "update" is not useful because it gives no information about what was changed. A longer message body is useful when the reason for a change needs additional explanation.


Remotes and the everyday workflow
6. Explain the relationship between your local repository and origin. What do push and pull each move, in which direction, and why is pulling before pushing the habit to build?

ANS : My local repository is the Git repository on my computer, while origin usually refers to the remote repository on GitHub. 
git push sends local commits to the remote repository, while git pull brings remote changes into the local repository. 
Pulling before pushing helps me work with the latest changes and reduces conflicts.


7. git fetch and git pull are not the same command. What is the difference, and when would you deliberately choose fetch?

ANS : git fetch downloads changes from the remote repository without automatically merging them into my current branch. git pull downloads the changes and then integrates them into my current branch. 
I would use fetch when I want to inspect remote changes before deciding how to integrate them.


Branching, merging, pull requests
8. A branch in Git is often described as "just a pointer." Explain what that means, and explain concretely what goes wrong on a team when everyone commits directly to main.

ANS : A branch is basically a pointer to a line of commits that lets me work separately from another branch. 
If everyone works directly on main, unfinished or conflicting changes can affect the shared code. Using separate branches allows developers to work on features independently before merging them.


9.  A merge conflict happens when two branches change the same lines of the same file. Explain why Git cannot resolve this automatically, what the 
<<<<<<< , ======= , >>>>>>> markers mean, and what you must do to finish the merge.

ANS: A merge conflict happens when two branches change the same lines of the same file and the git cannot resolve this automatically because Git cannot automatically decide which changes should be kept in file. It will be confused which version is correct between those file.

<<<<<<< HEAD
This marks the beginning of the conflict section.
=======
This separates our branch's change from the incoming branch changes
>>>>>>> branch-name
This marks the end of the conflict.

I must manually choose or combine the correct changes, remove the markers, save the file, stage it, and complete the merge.

Example:
<<<<<<< HEAD
print("Hello from main branch")
=======
print("Hello from feature branch")
>>>>>>> feature



 10. You could merge a branch locally with git merge and push. What does opening a Pull Request add that a local merge does not? What belongs in a PR description?

ANS : A Pull Request allows other team members of the following projects to review changes before they are merged into the main branch. It provides a place for discussion, review, testing, and feedback. 
A PR description should explain what was changed in the file, what was the reason behind the changes, or any other issue that came or testing information.


ISSUES
11. Explain the purpose of labels and assignees on an Issue, and what Fixes #12 in a merged PR does. Why is linking work to Issues better than closing them by hand?

ANS : Labels are tags that help organize Issues by categories such as bug, feature, documentation, and so on. Teams can quickly see what type of work an issue represents and prioritize accordingly.
Assignes show who is responsible for solving the issue. This avoids the confusion about ownership and ensures accountability.

When we writes Fixes #12 in PR. Github automatically links the PR to issue #12 and once the PR is merged, Issue #12 is automatically closed.

Linking work to Issues keeps project history organized and makes it easier to track completed work.


Project structure, environments, secrets
12. Why should .gitignore be one of your first commits? If a file is already tracked, does adding it to .gitignore stop Git from tracking it — and if not, what do you do instead?

ANS : .gitignore should be created early because files such as virtual environments, temporary files, and secrets are not accidentally committed. 
It stops unnecessary files from ever entering version control. 
Adding a file to .gitignore does not stop Git from tracking a file that is already tracked. For an already tracked file, I need to remove it from tracking with something like 
git rm --cached filename.
git commit -m "Stop tracking filename"


13. Explain the difference between .env and .env.example , and why they get opposite treatment. If a real API key was committed three weeks ago, why is deleting it in a new commit not a fix, and what should actually be done?

ANS : 
A .env file contains real, sensitive environment variables such as API keys, database passwords which should never be committed to Git.
A .env.example contains example variable names and placeholder values so other developers know what they need to configure.
If a Real API Key was committed then deleting it in a new commit is not a fix because:
- Git history is permanent so the secret still exists in earlier commits
- Anyone who cloned or forked the repo can still see it.
- Even if we delete it, the leak has already happened.

What should actually be done are:
- Revoke the exposed key immediately through our API provider's dashboard.
- Generate a new key and update our .env file locally.
- Add .env to .gitignore so it doesn't happen again.


14. What problem do a virtual environment and requirements.txt solve together? Why is venv/ itself never committed, when requirements.txt always is?

ANS : A virtual environment keeps a project's Python packages isolated from other projects. requirements.txt records the packages and versions needed to recreate that environment. 
The venv/ folder should not be committed because it contains environment-specific files, while requirements.txt should be committed so other developers can install the required dependencies.


15. Explain what venv/ itself git push --force does to a shared branch and whose work it can destroy. How does -- force-with-lease behave differently, and why is that safer? 

ANS : git push --force overwrites the remote branch with our local branch, removing whatever was on the remote. On the shared branch, this can destroy teammate's commits if they pushed after you last pulled. Rewrite history in a way that makes other's work disappear.
git push --force-with-lease is safer alternative. It only overwrites the remote branch if no one else has pushed new commits since you last fetched. If someone else has updated the branch, your push will be rejected instead of destroying their work.











