# Dataset Registry Server
Dataset registry for multiple DVC projects.

To add new datasets:
- clone this repository
- create a new folder with the same name as the GitHub repository (`github-repo`)
- copy the project data inside the folder `<github-repo>`
- inside `<github-repo>` run the command: `dvc add .`
- create a new remote storage (in this case inside your Dropbox folder):
  ```bash
  mkdir ~/Dropbox/dataset-storage/<github-repo>
  dvc remote add -d dropbox-storage-<github-repo>  ~/Dropbox/dataset-storage/<github-repo>
  ```
- push to the data to the selected dataset storage:
  ```bash
  cd <github-repo>
  dvc push -r dropbox-storage-<github-repo>
  ```
