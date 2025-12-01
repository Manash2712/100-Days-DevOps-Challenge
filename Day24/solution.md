### Solution

Follow the below steps for this task.

- Login to storage server.
  ```
  ssh natasha@ststor01
  ```
- Change the working directory to /usr/src/kodekloudrepos/games.
  ```
  cd /usr/src/kodekloudrepos/games
  ```
- Lets check the current branch.
  ```
  git branch
  ```
- If current branch is not master use below to change it to master.
  ```
  git checkout master
  ```
- Now create a branch from master.
  ```
  git checkout -b xfusioncorp_games
  ```
