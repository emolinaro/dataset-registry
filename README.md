# Dataset Registry Server
Dataset registry for multiple DVC projects.

## Add data to the dataset registry

To add new datasets used in a DVC project repository on GitHub:

- Create a new folder with the same name as the GitHub repository `<github-repo>` where the project source code is stored.
- Copy the `<project-data>` inside the folder `<github-repo>`.
- Inside `<github-repo>` run the command: `dvc add <project-data>`; this will create a new DVC-File, which is a pointer to the real dataset.
- Create a new remote dataset storage:
  ```bash
  dvc remote add -d abacus-storage-<github-repo> ssh://fe.deic.sdu.dk:/work/sduescience/molinaro/dataset-storage/<github-repo>
  dvc remote modify abacus-storage-<github-repo> user molinaro
  dvc remote modify abacus-storage-<github-repo> port 22
  dvc remote modify abacus-storage-<github-repo> keyfile ~/.ssh/id_rsa
  ```
- `git commit` the new DVC-File.
- Push the data to the selected dataset storage:
  ```bash
  cd <github-repo>
  dvc push DVC-File -r abacus-storage-<github-repo>
  ```
- (Optional) Remove the data folder inside `<github-repo>`; the latter can be recovered from the dataset storage with the command: `dvc pull /path/to/DVC-File`.
- (Optional) Change cache directory:
  ```bash
  dvc cache dir /tmp/cache
  ```
## Import data from the dataset registry

To import and track one of the datasets from the dataset storage to a GitHub repository `<github-repo>`:

- Clone `<github-repo>` from GitHub.
- Run the command `dvc init` in case `<github-repo>` is not a DVC repository.
- Run the command: 
  ```bash
  dvc get -o /destination/path https://github.com/emolinaro/dataset-registry <github-repo>
  ```
  Use the flag `--rev` to select a specific branch, tag, or commit.
- Set remote storage:
  ```bash
  dvc remote add -d abacus-storage-<github-repo> ssh://fe.deic.sdu.dk:/work/sduescience/molinaro/dataset-storage/<github-repo>
  dvc remote modify abacus-storage-<github-repo> user molinaro
  dvc remote modify abacus-storage-<github-repo> port 22
  dvc remote modify abacus-storage-<github-repo> keyfile ~/.ssh/id_rsa
  ```
 - (Optional) Change cache directory:
  ```bash
  dvc cache dir /tmp/cache
  ```
