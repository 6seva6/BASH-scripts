## Scenario: Check Response Codes of Links from a File

Objective: We have a file containing a list of URLs. Our task is to check the response codes for each link.

Requirements:
    - If a link returns a status code greater than 400 and less than 599, indicating an unavailable response, stop further checks immediately.
    - The entire process must complete within a time limit of 1 minute.
    
```bash
#!/usr/bin/env bash
#The scripta work properly if following conditions matched:
#-Every link begin from new line
#-No empty line in the list

# 1. Scecyfing file path to the links
read -p "Specify the Path to the File Containing Links:" file_path

# 2. Check the file path is not null
if [[ -z "$file_path" ]]; then
  echo "[ERROR] File Path Not Specified, please specify the file path."
  exit 1
fi

# 3. Check if file exists
if [[ ! -f "$file_path" ]]; then
  echo "[ERROR] The file does not exist: $file_path"
  exit 1
fi
# 4. Check if file is not empty
if [[ ! -s "$file_path" ]]; then
  echo "[ERROR] The file is empty: $file_path"
  exit 1
fi

# 5. Script start time and time limit
start_time=$(date +%s)
TIME_LIMIT=60  

# 6. Function to check time limit

check_time_limit() {
  local now=$(date +%s)
  local elapsed=$(( now - start_time ))

  if (( elapsed >= TIME_LIMIT )); then
    echo "[ERROR] Exceeded 1 minute. Exiting now."
    exit 1
  fi
}

# 7. Function that checks URLs

check_urls() {
  local file_path="$1"

  while read url; do

    check_time_limit

    echo "[INFO] Checking URL: $url"

    status_code=$(curl -s -o /dev/null -w "%{http_code}" "$url")

    if [[ "$status_code" -ge 400 && "$status_code" -le 599 ]]; then
      echo "[ERROR] URL '$url' status code $status_code. Stopping checks."
      return 1
    else
      echo "[OK] URL '$url' status code $status_code."
    fi

  done < "$file_path"

  return 0
}

# 8. Invoke the function with /urls.txt

check_urls "$file_path"
exit_code=$?

if [[ $exit_code -eq 0 ]]; then
  echo "[INFO] All URLs appear available."
else
  echo "[SUMMARY] One of URL was unavailable or time limit reached."
fi
```
