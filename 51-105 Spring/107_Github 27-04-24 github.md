* go to github and create a online repository
* open the file directory in cmd
* copy the code for push the code to online repository

![alt text](https://i.ibb.co/HgwLdKS/image.png)

* after paste the code and hit enter, a pop-up will show for github login 
* after login , push to main branch will done

```bash
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (5/5), 393 bytes | 393.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/shankarbhola/gittesting.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

### **Configure git in IntelliJ Idea**
* go to setting 

![alt text](https://i.ibb.co/z7tZFcm/image.png)

* initiate the git repository

![alt text](https://i.ibb.co/BqS2BnS/image.png)

* all files are in red
* to add all the files
* right click on project / git / add

![alt text](https://i.ibb.co/yV8b4RV/image.png)

* now all files becomes green and ready to commit
* then commit (right click on project / git / commit)
* give a meaningful mesage then commit
* to push from local to github, go to github and create a repository and copy the git link

![alt text](https://i.ibb.co/hMZFLq0/image.png)

- right click on project / git / push

![alt text](https://i.ibb.co/QXjmgXF/image.png)

* paste the git link then click ok

![alt text](https://i.ibb.co/t84q44P/image.png)

* push code to github

![alt text](https://i.ibb.co/ydGXFVd/image.png)

* now all your code pushed into github

![alt text](https://i.ibb.co/dPm3y6z/image.png)

### **Github in company**

* a github url will share by your company
* go to git / clone

![alt text](https://i.ibb.co/yPRg5VL/image.png)

* paste the url and click on clone

![alt text](https://i.ibb.co/k5kR5nn/image.png)

* one bug will share with you in bugzilla or clearquest or any other defect tracking tools
* every bug has a bug id
* suppose the fecect id is 1278 and the defect is accepting invalid email id
* before fix the code you can't modify the original code , so we keep the original one and modify copy of the project
* if we directly push the code in main branch , if some errors are in our code or any junior developer , then the total project will crashed 
* so we have to create a separate branch and push that code in to that new branch
* the purpose of creating a branch is, the project you got from the manager, the complete project will copy to in the new branch

![alt text](https://i.ibb.co/mTtvksp/image.png)

* branch name shod be the developeName-bugId-bugName

![alt text](https://i.ibb.co/1ZNwmZ5/image.png)

* switch from master branch to created new branch

![alt text](https://i.ibb.co/ScPbmWK/image.png)

* make sure you are in newly created branch

![alt text](https://i.ibb.co/hm2ssPX/image.png)

* now fix the bug or change some files 
* after fix the bug, commit the code
* you cannot commit whatever you want

![alt text](https://i.ibb.co/MGz1fgW/image.png)

* push code
* then manager will review the code and test , if the defect fixed then he will merge thw code with defect branch