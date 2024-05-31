### Why We Use Git ###

1. **Version Control:**
   - Tracks changes in code.
   - Allows reverting to previous versions.

2. **Branching and Merging:**
   - Work on different features separately.
   - Merge changes smoothly.

3. **Backup:**
   - Each copy of the repository is a full backup.

### Why We Use GitHub ###

1. **Remote Repository:**
   - Central place to host code online.
   - Accessible from anywhere.

2. **Collaboration:**
   - Pull requests for code reviews.
   - Issue tracking for bugs and tasks.

3. **Continuous Integration/Deployment (CI/CD):**
   - Automate testing and deployment.

4. **Documentation:**
   - Easy to add and maintain project documentation.

### Problems Solved by Git and GitHub ###

1. **Code Management:**
   - Keeps track of code changes and history.

2. **Team Collaboration:**
   - Multiple people can work together without conflicts.

![alt text](https://i.ibb.co/tpWY6Rj/image.png)

3. **Conflict Resolution:**
   - Tools to handle simultaneous changes by different developers.

4. **Backup and Safety:**
   - Prevents code loss with multiple backups.

5. **Code Quality:**
   - Ensures code is reviewed and meets standards.

6. **Project Management:**
   - Organizes tasks and tracks progress.

7. **Automation:**
   - Automatically tests and deploys code.

8. **Community Contributions:**
   - Easy for others to contribute to open-source projects.

In Git, the process of selecting files to back up (commit) is handled in a few steps:

## Steps to Back Up Files in Git and View Commit History ##

1. **Navigate to your project directory:**

```bash
cd my-files-backup
```

2. **Initialize a new Git repository (if not already initialized):**

```bash
git init
```

**Output:**
```bash
Initialized empty Git repository in /path/to/my-files-backup/.git/
```

3. **Stage specific files for backup:**

Sure, here's the sequence of commands along with their outputs:

4. **Add A.txt**

```bash
git add A.txt
```

*No output is shown for this command.*

5. **Commit Changes**
```bash
git commit -m "Add A.txt"
```

**Output:**
```bash
[main (root-commit) 1a2b3c4] Add A.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 A.txt
```

6. **View Commit Log**
```bash
git log
```

**Output:**
```bash
commit 1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p7q8r9s0
Author: Your Name <your.email@example.com>
Date:   Sat May 25 14:32:21 2024 +0000

    Add A.txt
```

7. **Add B.txt and C.txt**

```bash
git add B.txt C.txt
```

*No output is shown for this command.*

8. **Commit Changes**
```bash
git commit -m "Add B.txt and C.txt"
```

**Output:**
```bash
[main 5t6u7v8] Add B.txt and C.txt
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 B.txt
 create mode 100644 C.txt
```

9. **View Commit Log**
```bash
git log
```

**Output:**
```bash
commit 5t6u7v8w9x0y1z2a3b4c5d6e7f8g9h0i1j2k3l4
Author: Your Name <your.email@example.com>
Date:   Sat May 25 15:12:34 2024 +0000

    Add B.txt and C.txt

commit 1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p7q8r9s0
Author: Your Name <your.email@example.com>
Date:   Sat May 25 14:32:21 2024 +0000

    Add A.txt
```
