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
