# Backup and archiving

## Scenario: Backup Specific Files by Suffix

  We need to back up specific files with a designated suffix from a directory. To accomplish this, the following steps are required:
  
  - Collect Information:
      - Obtain the path where the search will be conducted.
      - Identify the desired file suffix.
      - Determine the directory where the backups will be stored.
  
  - Create a Backup Folder:
      - Establish a dedicated folder to store the backed-up files.
  
  - Search and Store Files:
      - Locate and transfer the files with the specified suffix to the backup folder.
  
  - Archive the Data:
      - Compress the collected files into an archive for efficient storage.
        
  - Solutions:
    
```bash
#!/bin/bash
# Author: Vsevolod
# Script to prompt to back up files
# Files will be searched in specyfied path and backed up to a directory within $HOME  

read -p "Please scpecify the path to the folder for backups: " path
read -p "Pleace specify file type do you want to back up (.txt;.sh;.conf): " file_suffix
read -p "Please specify the directory do you want to backup to: " dir_name

# Test for directory existing if it does not exist, create it
test -d $HOME/$dir_name || mkdir -m 700 $HOME/$dir_name

# Exclude the created directory from the search and find the desired file types in the specified path.
find $path -path $HOME/$dir_name -prune -o \
-name "*$file_suffix" -exec cp {} $HOME/$dir_name/ \;
# Archive the folder
tar -czvf "$HOME/$(date +%d-%m-%Y)_${dir_name}.tar" "$HOME/$dir_name" && rm -r $HOME/$dir_name/
exit 0 
```
