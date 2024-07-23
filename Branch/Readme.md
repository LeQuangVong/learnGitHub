## Main branch ```Master```
### Create with 3 commit:
```
git log --oneline
d8e1fc6 (HEAD -> master) C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
### List of branches
```
git branch
* master
```
There is a branch, the symbol * indicates that (cho biết) this is the current branch.
### Create new branch
```
git branch alpha
```
Check branch:
```
git branch
  alpha
* master
```
The HEAD pointer remains on the ```master``` branch, ```alpha``` branch starts from ```C2``` commit (inheriting (kế thừa) master from C2 and earlier).

![branch alpha master](./gitbranch-4307.png)
### Change working branch
```
git checkout alpha
#or
git switch alpha
```
Check branch:
```
git branch
* alpha
  master
git log --oneline
d8e1fc6 (HEAD -> alpha, master) C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
Both ```master``` and ```alpha``` are pointing to ```C2``` commit but the HEAD pointer indicates (cho biết) working on the ```alpha``` branch.
![](./gitbranch-4308.png)

### Make a commit on ```alpha``` branch
```
git log --oneline
06e9842 (HEAD -> alpha) C3
d8e1fc6 (master) C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
```alpha``` branch has a ```C3``` commit and inherits old commits from ```master``` (C0,C1,C2) starting from ```C2``` .
![](./gitbranch-4309.png)

Next create commit on ```alpha``` branch:
```
git log --oneline
6a48924 (HEAD -> alpha) C4
06e9842 C3
d8e1fc6 (master) C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
![](./gitbranch-4310.png)

### Switch back to work on the ```master``` branch and create a new commit here
```
git checkout master                                                   
Switched to branch 'master'
git status                                                   
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Branch/

nothing added to commit but untracked files present (use "git add" to track)

git add .     

git commit -m"C5"                                                   
[master 67e4edf] C5
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 Branch/gitbranch-4310.png

 git log --oneline
 67e4edf (HEAD -> master) C5
d8e1fc6 C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
![](./gitbranch-4310.png)

### Create new branch from master
The code in the ```master``` needs to be edited and tested immediately, with the hope that during the process of modifying the code and checking errors, it will not mess up the lines of code being worked on with the ```master```, so a new branch can be immediately created:
```
git branch sualoigap        #create new branch
git checkout sualoinhanh    #switch branch
```
Check branch:
```
git log --oneline
67e4edf (HEAD -> sualoigap, master) C5
d8e1fc6 C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
![](./gitbranch-4320.png)

HEAD pointer indicates working on the ```sualoigap``` branch.

Next create a commit on ```sualoigap``` branch:
```
git log --oneline
f1ee977 (HEAD -> sualoigap) C7
2815cd4 C6
67e4edf (master) C5
d8e1fc6 C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
![](./gitbranch-4322.png)

## Branch Merge
Merge the ```sualoigap``` branch into the ```master``` branch:
```
git checkout master                                                   
Switched to branch 'master'
git merge sualoigap                                                
Updating 67e4edf..5b0d8cc
Fast-forward
 Branch/1.txt              |   2 ++
 Branch/gitbranch-43.png   | Bin 0 -> 27542 bytes
 Branch/gitbranch-4320.png | Bin 0 -> 31197 bytes
 Branch/gitbranch-4322.png | Bin 0 -> 37280 bytes
 4 files changed, 2 insertions(+)
 create mode 100644 Branch/1.txt
 create mode 100644 Branch/gitbranch-43.png
 create mode 100644 Branch/gitbranch-4320.png
 create mode 100644 Branch/gitbranch-4322.png

git log --oneline
5b0d8cc (HEAD -> master, sualoigap) C7
2815cd4 C6
67e4edf C5
d8e1fc6 C2 - Update,Readme.md
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
![](./gitbranch-4323.png)

## Delete branch
Delete ```sualoigap``` branch:
```
git branch
  alpha
* master
  sualoigap

git branch -d sualoigap                                                
Deleted branch sualoigap (was 5b0d8cc).

git branch
  alpha
* master
```
![](./gitbranch-4331.png)

## Handle conflicts when merging branches
Now we merge the ```alpha``` branch into the ```master``` branch because both branches have many commit since the branch time (thời điểm rẽ nhánh), so when merging, git does not automatically create new commit and it pauses so we can processes each (từng) conflicting file and create issue a commit after resolvign all conflicts (xung đột).
```
git merge alpha                                                    
CONFLICT (add/add): Merge conflict in Branch/Readme.md
Auto-merging Branch/Readme.md
CONFLICT (add/add): Merge conflict in Branch/1.txt
Auto-merging Branch/1.txt
Automatic merge failed; fix conflicts and then commit the result.

git status                                                   
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        new file:   Branch/gitbranch-4307.png
        new file:   Branch/gitbranch-4308.png
        new file:   Branch/gitbranch-4309.png

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      Branch/1.txt
        both added:      Branch/Readme.md

git add .                                                   

git commit -m"C8 - gop nhanh alpha"  

git status                                                   
On branch master
nothing to commit, working tree clean
```

Draw a detailed branch merging diagram:
```
git log --oneline --graph
*   eb2ef70 (HEAD -> master) C8 - gop nhanh alpha
|\  
| * 6a48924 (alpha) C4
| * 06e9842 C3
* | 7988423 C7
* | 2815cd4 C6
* | 67e4edf C5
|/  
* d8e1fc6 C2 - Update,Readme.md
* 81be31a C1 - Sua doi a.txt
* 126ad7f C0 - Khoi tao du an
1
```

![](./gitbranch-4332.png)

We can move the HEAD pointer to the last commit of the ```master``` branch before merging branch (C7) and ```alpha``` branch (C4).
```
git checkout 7988423   #7988423 is hash of C7 commit
git checkout 6a48924   #6a48924 is hash of C4 commit
```
## Git rebase
Create commits in two branches ```beta``` and ```master```
```
#beta branch
git log --oneline
74ab41d (HEAD -> beta) B2
086b1b6 B1
fa1423d C3
be90521 C2
f2d3245 C1

#master branch
git log --oneline
a621372 (HEAD -> master) D2
e5176f7 D1
fa1423d C3
be90521 C2
f2d3245 C1
```
Proceed to merge the ```beta``` branch into the ```master``` branch, standing at (đứng ở) the ```master``` to excute the command:
```
git rebase beta
* bbb0179 (HEAD -> master) D2
* c7cc53c D1
* 367d02d (beta) B2
* 4b16194 B1
* fa1423d C3
* be90521 C2
* f2d3245 C1
```
![](./git012.png)

### Difference between ```git merge``` and ```git rebase```
```Git merge```:
- Consider (xem xét) changes on 2 branches at 3 times: the last commit time of the branches and branch time.
- Commits are arranged in chronological order (thứ tự thời gian).

```Git rebase```:
- The common commits between two branches are called base commit.
- Put the entire ```beta``` branch as the master's base, so the next commits after the master's original base commit will be folowed, with changes to the commit history.

**NOTE:** Because rebase will rewrite the commit history on the branch, absolutely (tuyệt đối) do not schedule a rebase when the branch's commit have been pushed to the public Repository, otherwise (nếu không) everything will be messy (rối tung).
