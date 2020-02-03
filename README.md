# Dataset Registry Server
Dataset registry for multiple DVC projects.

To add new datasets used in other DVC repositories on GitHub:
- Create a new folder with the same name as the GitHub repository (`github-repo`) where the project source code is stored.
- Copy the project data inside the folder `<github-repo>`.
- Inside `<github-repo>` run the command: `dvc add .`; this will create a new DVC-file, which is a pointer to the real dataset.
- Create a new remote storage (in this case inside your Dropbox folder):
  ```bash
  mkdir ~/Dropbox/dataset-storage/<github-repo>
  dvc remote add -d dropbox-storage-<github-repo>  ~/Dropbox/dataset-storage/<github-repo>
  ```
- `git commit` the new DVC-file.
- Push to the data to the selected dataset storage:
  ```bash
  cd <github-repo>
  dvc push -r dropbox-storage-<github-repo>
  ```
- (Optional) remove the data folder inside `<github-repo>`; the latter can be recovered from the dataset storage with the command: `dvc pull /path/to/DVC-file`.
