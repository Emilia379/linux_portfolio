# Data Filtering and Manipulation Exercises with `grep` and Pipes

This section explores the use of `grep` commands to filter specific data from log files and `pipe` (`|`) to concatenate commands, allowing for more complex analysis.

![Nuova schermata esercizi Grep e Pipe](/images/nuova_grep_pipe.png)

### 1. Searching for Errors in Logs:
* **Objective:** To find all occurrences of the string "error" in the `server_logs.txt` file.
* **Command:** `grep 'error' server_logs.txt`
* **Output Example:**
    ```
    2022-09-28 13:56:22 error The password is incorrect
    2022-09-28 15:56:22 error The username is incorrect
    2022-09-28 16:56:22 error The password is incorrect
    2022-09-29 13:56:22 error An unexpected error occurred
    2022-09-29 15:56:22 error Unauthorized access
    2022-09-29 16:56:22 error Unauthorized access
    ```
* **Explanation:** The `grep 'pattern' file` command searches for lines that contain the exact 'pattern' specified.

### 2. Specific User Search in Reports:
* **Objective:** To search for the string "users" in the `/home/analyst/reports` directory.
* **Command:** `ls /home/analyst/reports | grep users`
* **Output Example:**
    ```
    Q1_added_users.txt
    Q1_deleted_users.txt
    ```
* **Explanation:** The `pipe` (`|`) redirects the output of the `ls` command as input for `grep`, which then filters lines containing "users".

### 3. Searching for Specific Strings Within File Names:
* **Objective:** To find files in the current directory that contain the string "Q1".
* **Command:** `ls | grep Q1`
* **Output Example:**
    ```
    Q1_access.txt
    Q1_added_users.txt
    Q1_deleted_users.txt
    ```
* **Explanation:** Similar to the previous example, this shows how to filter `ls` output to find specific file names.

### 4. Searching for a Specific User in a Report File:
* **Objective:** To find information about user "jhill" in the `Q2_deleted_users.txt` file.
* **Command:** `grep jhill Q2_deleted_users.txt`
* **Output Example:**
    ```
    1025 jhill Sales
    ```
* **Explanation:** `grep` can be used to search for specific strings within a file's content.

### 5. Searching for a Specific Department in a Report File:
* **Objective:** To find all users in the "Human Resources" department in the `Q4_added_users.txt` file.
* **Command:** `grep "Human Resources" Q4_added_users.txt`
* **Output Example:**
    ```
    1151 sshah Human Resources
    1145 msosa Human Resources
    ```
* **Explanation:** Useful for extracting specific data based on a criterion.

### 6. Counting Error Occurrences (Additional Example):
* **Objective:** To count how many times the word "error" appears in the `server_logs.txt` file.
* **Command:** `grep -c 'error' server_logs.txt`
* **Output Example:** `6`
* **Explanation:** The `-c` option of `grep` returns only the count of lines containing the pattern.

## Advanced Search with `find`

This section explores the use of the `find` command for locating files and directories based on various criteria.

### 1. Searching Files by Name:
* **Objective:** To find all files with a `.txt` extension in the current directory and its subdirectories.
* **Command:** `find . -name "*.txt"`
* **Output Example:**
    ```
    ./logs/server logs.txt
    ./reports/users/Q1_access.txt
    ./reports/users/Q1_added_users.txt
    ./reports/users/Q1_deleted_users.txt
    ```
* **Explanation:** The `find .` command starts the search from the current directory. The `-name "*.txt"` option searches for files whose name matches the pattern (all 
files with a `.txt` extension).

### 2. Searching Files by Size:
* **Objective:** To find all files larger than 1 Megabyte (`1M`) in the current directory and its subdirectories.
* **Command:** `find . -size +1M`
* **Output Example:**
    ```
    ./large_data_file.zip
    ./old_backup.tar.gz
    ```
* **Explanation:** The `-size` option allows filtering by size. `+1M` means "larger than 1 Megabyte".

### 3. Searching and Executing Commands:
* **Objective:** To combine `find` with `-exec` to run a command on the found files (e.g., search for a specific keyword in all `.txt` files).
* **Command:** `find . -name "*.txt" -exec grep "keyword" {} \;`
* **Explanation:** This command first finds all `.txt` files. For each found file (`{}`), it then executes `grep "keyword"` on that file. The `\;` marks the end of the 
`-exec` command.
    *(Note: This example doesn't have a specific output shown, as it depends on whether "keyword" is found in your files. It's more of a functional demonstration.)*
---
## Reflections and Future Improvements

This exercise represents a starting point for log analysis. In the future, I could extend this exercise to:
* Filter logs by severity level (e.g., only `error` or `warning`) using `grep`.
* Count the occurrences of specific events.
* Automate these operations with a Bash script.
---
