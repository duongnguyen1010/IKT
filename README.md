## Exercise 1: Racap Resolve Merge Conflicts
<img width="459" height="155" alt="image" src="https://github.com/user-attachments/assets/a3bcca90-586a-4e8b-9f6a-921d46695612" />

+ For more information, please check the commits

## Exersise 2: Recovery Scenarios
###
+ wrong content:
  `Hier ist test!
main Änderung hier!
change from feature-x
wrong change!`

for this case i used `git checkout HEAD^ -- file.txt` which is go back to the last commit(11f0b8f). After this i commit again
to have the right commit but team are able to see those commits

+ Content after:
  `Hier ist test!
main Änderung hier!
change from feature-x`

<img width="763" height="214" alt="image" src="https://github.com/user-attachments/assets/2fad0524-e59a-42b3-818f-2f7a3bb7dc0f" />


### Scenario B: `git reset`
+ terminal code:
```
❯ touch file2.txt
❯ git add .
❯ git commit -m "main: add file2.txt"
[main f00a474] main: add file2.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 assignment3b/file2.txt
❯ git log --oneline --graph
```
+ Git log before soft and hard reset.

<img width="643" height="245" alt="image" src="https://github.com/user-attachments/assets/ebfb43a7-a3f8-466b-87d4-789862b44f11" />

+ Soft reset:
```
❯ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
❯ git reset --soft HEAD~1
❯ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   file2.txt

~/Desktop/home/Aktuelle Trend Inf/homeworks/assignment3b main* ❯
```
The commit is deleted but the change is still added.

+ hard Reset

```
❯ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
❯ ls
file.txt  file2.txt
❯ git reset --hard HEAD~1
HEAD is now at 4a46c8e Merge branch 'main' of github.com:duongnguyen1010/IKT
❯ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
❯ ls
file.txt
```
Commit is deleted incluve also the file2.txt

### Scenario C: `git revert`

+ Git log after mistake
<img width="652" height="249" alt="image" src="https://github.com/user-attachments/assets/10ec90d5-5da4-471f-9d4c-d05596dcffc7" />

+ Git command:

```
❯ git log --oneline
❯ git revert 4a46c8e
error: commit 4a46c8eaef5d2e0c29d00de149e336ddaceb35e8 is a merge but no -m option was given.
fatal: revert failed
❯ git revert -m 1 4a46c8e
[main 2fe354a] Revert "Merge branch 'main' of github.com:duongnguyen1010/IKT"
 1 file changed, 11 deletions(-)
 delete mode 100644 README.md
❯ git log --oneline
```
+ Log after revert
```
2fe354a (HEAD -> main) Revert "Merge branch 'main' of github.com:duongnguyen1010/IKT"
6ffdcd1 main: oops line deleted
4a46c8e (origin/main) Merge branch 'main' of github.com:duongnguyen1010/IKT
5ce58e7 Create README.md for Report
6f71a57 main: correct version of file.txt from previous commit
45761ae main: wrong change on main
11f0b8f main: merge feature-x to main
71f05ae main: main änderung
f318a0f (feature-x) feature-x: change file.txt
bdb21db first commit
```
In my case there was an error when i try to use revert because git didn't know which parent should the commit be jump to latest. so i need to add the -m(mainline) 1 as main and then the commit id.

