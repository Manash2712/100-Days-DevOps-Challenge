### Solution

This is a relatively simple task follow the below steps to perform this task.

- Login to the storage server.
  ```
  ssh natash@ststor01
  ```
- Install git.
  ```
  yum install git -y
  ```
- Create a dir in /opt with name ecommerce.git
  ```
  mkdir /opt/ecommerce.git
  ```
- Change the working directory to the above created directory
  ```
  cd /opt/ecommerce.git
  ```
- Use below command to initialize a bare repository.
  ```
  git init --bare
  ```

#### Notes:
A bare Git repository is a type of Git repository that does not contain a working directory or a working tree. This means it lacks the actual project files that you would edit and interact with directly. Instead, a bare repository only contains the Git metadata and internal data structures that manage the project's version control history.
Here are the key characteristics and uses of bare repositories:
- __No Working Directory:__ Unlike a standard Git repository (which has a .git subdirectory and the project files alongside it), a bare repository is essentially the contents of what would normally be inside the .git directory. The files like branches, config, description, HEAD, and objects are found directly in the repository's root.
- __Remote Repository:__ Bare repositories are primarily used as centralized remote repositories for collaborative development. Services like GitHub, GitLab, and Bitbucket effectively host bare repositories.
- __No Direct Development:__ You cannot directly edit files, create new commits, or perform operations like git status or git commit within a bare repository because there is no working copy of the files to interact with.
- __Push and Pull Operations:__ Their purpose is to serve as a hub for developers to push their changes to and pull updates from, facilitating code sharing and synchronization among team members.
- __Creation:__ A bare repository is typically created using the git init --bare command.
  
In essence, a bare repository acts as a clean, central storage point for the project's history, without the overhead and potential conflicts of a working directory, making it ideal for managing shared codebases.
