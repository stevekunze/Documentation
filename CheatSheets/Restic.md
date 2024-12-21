# general cheatsheet for frequently used commands

| command                                                                                                                                           | discription                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| restic init -r */path/to/repo/*                                                                                                                   | initialize restic repository on in desired path                                                                     |
| restic -r */path/to/repo/* backup */path/to/data/that* --compression=max                                                                          | backup files to repo with max compression                                                                           |
| restic -r */path/to/repo* check                                                                                                                   | check health status of repo                                                                                         |
| restic -r */path/to/repo* snapshots                                                                                                               | list snapshots                                                                                                      |
| restic -r */path/to/repo* ls *snpashot_id*                                                                                                        | lists all files of the specified snaphots (use pipe less, pipe fzf or redirect to a file for better readability)    |
| restic -r */path/to/repo* mount */path/to/mountpoint*                                                                                             | mount your entire repo to a specified location. Only works on Linux                                                 |
| restic -r *sftp://yourdoamain.example:/repo_name* --password-file */path/to/file* backup */path/to/source* --compression=max --tag *created file* | backup by using sftp using max compression and setting a tag.                                                       |
| restic -r *sftp://yourdoamain.example:/repo_name* --password-file */path/to/file* backup */path/to/source* --compression=max --tag *name of host* | define a host to prevent long rescans.                                                                              |
| restic -r sftp://yourdoamain.example:/repo_name --password-file */path/to/file* backup */path/to/source* --exclude-file *"/path/to/exclude.txt"*  | place txt file with unwanted files and folder in specified directory and                                            |
| restic -r sftp:host:reponame --password-file */path/to/file* forget --keep-daily 14 --keep-weekly 4 --keep-monthly 6  --keep-yearly 1 --prune     | host = host defined in .ssh/config file. Sets up a prune rule und runes a prune job according to hose defined rules |



