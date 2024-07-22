# Local Repository
## Create Local Repo
```
git init                                                                                                           ✔ 
Initialized empty Git repository in /mnt/e/workspace/GitHub/.git/
```
Then ```GitHub``` folder has became ```local Repository```, ```.git``` folder constains (bao gồm) all Git data about this Repo.

## Start monitoring (giám sát) files in the working directory
### Enter the command to check the status of the working directory:
```
git status                                                                                         ✔ 
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Readme.md
        localRepo/
        remoteRepo/

nothing added to commit but untracked files present (use "git add" to track)
```
```On branch master```: đang ở trên nhánh master, đây là nhánh chính mặc định được tạo ra.
```No commits yet```: chưa lưu 1 data nào vào git cả.
```Untracked files ...```: Trong thư mục làm việc có những file chưa được Git theo dõi, muốn Git theo dõi thì thực hiện lệnh ``` git add <file> ```

![life cycle](./lifecycle.jpg)

- The life cycle of the file in Git, first the new file is in an ```untracked``` state (no version monitoring).
- From the ```untracked``` state, use Git command to put it into a ```staged``` state, which means the file is included in the plan to save and start tracking (theo dõi).
- In the ```staged``` state, use Git command to update the Git database, called ```commit```. After updating, complete information about the file in the final version already exists (đã tồn tại) in the Git database and the file will be in ```unmodefied``` state.
- Or in the ```unmodefied``` state, the file will be deleted from the Git database to return to the ```untracked``` state.
### Put the new file into ```staged``` state
To ```a.txt``` into monitoring, use this command:
```
git add a.txt
```
Review status:
```
git status                                                                                      ✔ 
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Readme.md
        localRepo/
        remoteRepo/
```
The current state is that the file has been put into the ```staged area```, which is where the data will ```commited``` and writen to the ```Git database```.
Also to put into ```staged area``` quickly use some special cases like:
```
git add *.c    #add all files with .c extension
git add .      #add all changes, except delete files
git add -A     #add all changes
```
Example with command ```git add .```:
```
git status                                                                                         ✔ 
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md
        new file:   a.txt
        new file:   localRepo/lifecycle.jpg
        new file:   localRepo/localRepo.md
        new file:   remoteRepo/remoteRepo.md
```

So the entire (toàn bộ) project has 5 files that have been put into the ```staged area``` ready to make the fisrt ```commit```.

### Make the first commit
Committing is the operation (thao tác) of putting all content in the ```staged area``` into the Git database.
If committed, it changes the file from ```staged``` state to ```unmodified``` state.
Make ```commit``` with this command:
```
git commit -m"C0 - Khoi tao du an"
[master (root-commit) 126ad7f] C0 - Khoi tao du an
 5 files changed, 55 insertions(+)
 create mode 100644 Readme.md
 create mode 100644 a.txt
 create mode 100644 localRepo/lifecycle.jpg
 create mode 100644 localRepo/localRepo.md
 create mode 100644 remoteRepo/remoteRepo.md
```
```126ad7f``` is a 40-characters ```hash``` code used to indicate a certain ```commit```

### View commit history
```
git log
commit 126ad7feff33f47b759c382d38fbad4031ae4229 (HEAD -> master)
Author: LeQuangVong <vongoke@gmail.com>
Date:   Mon Jul 22 15:44:51 2023 +0700

    C0 - Khoi tao du an
```
It say the following:
- In the master branch there is 1 commit with hash code ```126ad7feff33f47b759c382d38fbad4031ae4229```
- ```HEAD``` is called a pointer in Git, the ```HEAD``` pointer is now in the ```master``` branch and the Repo has C0.
- Displays ```commit``` execytion (thực hiện) time, message content.

Check Repo status:
```
git status                                                  
On branch master
nothing to commit, working tree clean
```
```working tree clean``` mean: nội dung trong thư mục làm việc và nội dung lưu trong commit không có gì khác nhau, toàn bộ nội dung trong thư mục làm việc đã được lưu trữ an toàn vào Git.
### Restore file
We delete the a.txt file, check the working directory staus:
```
git status                                                   
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
There is a notification that the a.txt file has been deleted.
So if we want to restore the a.txt file, we use the command:
```
git restore a.txt   #restore specific file
#or
git restore .       #restore all file deleted
```
```
git restore a.txt                                                      
ls                                                       
Readme.md  a.txt  localRepo  remoteRepo
```
### Git diff
```git diff``` command is a command used to compare (so sánh) the content (nội dung) in the working directory, staged and the final commit.
Modify ```a.txt``` file:
```
git status                                                   
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
Compare:
```
git diff
diff --git a/a.txt b/a.txt
index 7c4a013..1802a74 100644
--- a/a.txt
+++ b/a.txt
@@ -1 +1,3 @@
-aaa
\ No newline at end of file
+aaa
+bbb
+ccc
```
Displays the original content (in the last commit) and the modified version.

Save the modified file to Git database:
```
git add .                                                    
git status                                                   
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt

git commit -m"C1 - Sua doi a.txt"                                                     
[master 81be31a] C1 - Sua doi a.txt
 1 file changed, 3 insertions(+), 1 deletion(-)

git status                                                   
On branch master
nothing to commit, working tree clean
```
### Git checkout
Create 1 commit C2: Update:
```
git commit-m "C2 - Update"
```
```
git log --oneline
1bcbe82 (HEAD -> master) C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
The HEAD pointer is currently at commit 3.
If we want to restore the a.txt file from the previous modification, we use command:
```
git checkout 126ad7f -- a.txt 
```
Current working directory status:
```
git status                                                  
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   localRepo/localRepo.md
```
Do not allow files to enter the staged area, we use command:
```
git restore --staged a.txt
```
Return to the last commit:
```
git checkout .          #Return all files
#or
git checkout --a.txt    #Return file a.txt
```
### .gitignore
In the project directory there may be files that you do no want git to monitor, so declare them in a file called ```.gitignore```
- Creted file ```.gitignore```
- Open file and update content into the ```.gitignore``` file:
```
b.txt
*.log
build/Release
```
Make an additional commit to commit "C2 - Update":
```
git commit --amend -m"C2 - Update,.gitignore"
```
### Undo or Delete commit
Create additional commit "C3 - Tiep tuc sua a.txt":
```
e8c8de1 (HEAD -> master) C3 - Tiep tuc sua a.txt
9e7121a C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
Cancel the last commit with ```git reset``` command:
Once a commit has been made and the commit has not been pushed to the ```Remote Repo``` with ```git push``` command, we can cancel that commit in two cases with ```git reset```:
#### Git reset with ```--soft``` parameter:
In the case, the last commit will be canceled, the HEAD pointer will move to commit "C2 - Update", and at the same time (đồng thời), the changes of the last commit will be transferred to ```staging area``` to have the opportunity (cơ hội) to re-commit or modify with the following command:
```
git reset --soft HEAD~1                                                   
git status                                                   
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt
git log --oneline
9e7121a (HEAD -> master) C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
Re-commit:
```
git commit -m"C3 - Tiep tuc sua a.txt"                  
[master 50d1bd7] C3 - Tiep tuc sua a.txt
 1 file changed, 2 insertions(+)
git status                                                   
On branch master
nothing to commit, working tree clean
git log --oneline
50d1bd7 (HEAD -> master) C3 - Tiep tuc sua a.txt
9e7121a C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```

#### Git reset with ```---hard``` parameter:
When using the ```--hard``` parameter, the result is the same as using ```--soft``` parameter, the only difference is that the changed content of the last commit is not included in the ```staging area``` but is canceled:
```
git reset --hard HEAD~1
```
```
 git reset --hard HEAD~1                                                  
HEAD is now at 9e7121a C2 - Update
git log --oneline
9e7121a (HEAD -> master) C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
Re-commit:
```
git commit -m"C3 - Tiep tuc sua a.txt"                            
On branch master
nothing to commit, working tree clean
git log --oneline
9e7121a (HEAD -> master) C2 - Update
81be31a C1 - Sua doi a.txt
126ad7f C0 - Khoi tao du an
```
#### Cancel ```git add```:
If you used the ```git add``` command to update changes in ```staging area```, you can undo this operation by executing the command:
```
git restore .
```
If you want to destroy a specific file, you dont have to destroy the entrire file:
```
git restore -- <file name>
```
