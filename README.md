# BASH-scripts

In this repository, I store my case scenarios and BASH scripts to address them.  

## 📂 Repository Structure 

Each file contains:  
  - ✅ **Scenario description**
  - 📜 **BASH script**
  - ⚠️ **Errors encountered and their resolutions**  

This repository serves as a **learning resource** and a **proof of hands-on experience** with BASH.

# Scenarios:
## 1. Scenario: Check Response Codes of Links from a File
File name - check_urls_code

Objective: We have a file containing a list of URLs. Our task is to check the response codes for each link.

Requirements:
- If a link returns a status code greater than 400 and less than 599, indicating an unavailable response, stop further checks immediately.
- The entire process must complete within a time limit of 1 minute.
# Backup and archiving

2. Scenario: Backup Specific Files by Suffix
## File name - Backup

Objective: We need to back up specific files with a designated suffix from a directory. To accomplish this, the following steps are required:
  
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
