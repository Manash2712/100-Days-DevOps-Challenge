### Solution

Login into Storage server and run the following commands

```
cd /usr/src/kodekloudrepos
```
```
git clone /opt/beta.git
```

To clone a git repository from a local folder you can use git clone and the folder location.

The git clone command is used to create a copy of an existing Git repository. Several options can be used with git clone to customize the cloning process:

Basic Cloning:
- git clone <repository-url>: This is the most common way to clone a repository, downloading all files, branches, and commit history.
- git clone <repository-url> <directory>: Clones the repository into a specified local directory instead of a folder named after the repository.

Controlling Repository Content:
- --bare: Creates a bare repository, which contains only the Git version control data (the .git folder) and no working directory. This is often used for creating central repositories on servers.
- --mirror: Creates a mirror clone, which is a complete, exact copy of the remote repository, including all refs, branches, and configuration. Primarily used for creating full backups. 
- --single-branch: Clones only a single specified branch, reducing the size of the local repository.
- --depth <depth>: Creates a shallow clone with a limited commit history, specified by the <depth> number of recent commits. Useful for large repositories where full history is not immediately needed.
- --sparse: Instead of populating the working directory with all files, only populates the files present in the root directory. This can improve performance for very large repositories. 
- --recurse-submodules: After cloning, it initializes and clones any submodules present in the repository, based on a provided pathspec or all submodules if no pathspec is given. 
