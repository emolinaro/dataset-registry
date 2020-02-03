# Dataset Registry Server
Dataset registry for multiple DVC projects.

## Add data to the dataset registry

To add new datasets used in a DVC project repository on GitHub:

- Create a new folder with the same name as the GitHub repository (`github-repo`) where the project source code is stored.
- Copy the project data inside the folder `<github-repo>`.
- Inside `<github-repo>` run the command: `dvc add .`; this will create a new DVC-File, which is a pointer to the real dataset.
- Create a new remote storage folder (in this case inside your Dropbox folder):
  ```bash
  mkdir ~/Dropbox/dataset-storage/<github-repo>
  dvc remote add -d dropbox-storage-<github-repo>  ~/Dropbox/dataset-storage/<github-repo>
  ```
- `git commit` the new DVC-File.
- Push to the data to the selected dataset storage:
  ```bash
  cd <github-repo>
  dvc push -r dropbox-storage-<github-repo>
  ```
- (Optional) remove the data folder inside `<github-repo>`; the latter can be recovered from the dataset storage with the command: `dvc pull /path/to/DVC-File`.
## Import data from the dataset registry

To import and track one of the datasets from the dataset storage to a GitHub repository `<github-repo>`:

- Clone `<github-repo>` from GitHub.
- Run the command `dvc init` in case `<github-repo>` is not a DVC repository.
- Run the command: 
  ```bash
  dvc import -o /destination/path https://github.com/emolinaro/dataset-registry/tree/master/<github-repo>/DVC-File 
  ```
  or, if you do not want to track the dataset:
  ```bash
  dvc get -o /destination/path https://github.com/emolinaro/dataset-registry/tree/master/<github-repo>/DVC-File
  ```
