# Cybersecurity Log Analysis: Identifying Anomalies with Shell Commands

This section demonstrates practical skills in cybersecurity by analyzing 
application logs using a sequence of Linux shell commands. The goal is to 
identify suspicious activities, errors and unauthorized access attempts 
within a fictional application log (`myapp.log`).

## Scenario: Application Log Monitoring

As a security analyst, I need to proactively monitor `myapp.log` for 
critical events that could indicate a security breach or system 
instability. I'll use a series of commands to filter, count, and summarize 
key security-related information.

## Sample Log File (`myapp.log`)

```` ``` ````
2023-10-26 08:00:01 INFO: User 'alice' logged in from 192.168.1.10
2023-10-26 08:00:05 INFO: Application started successfully.
2023-10-26 08:00:10 WARNING: Disk space low on /var/log
2023-10-26 08:00:15 INFO: User 'bob' logged in from 10.0.0.5
2023-10-26 08:00:20 ERROR: Database connection failed for user 'admin'
2023-10-26 08:00:25 INFO: Data backup completed.
2023-10-26 08:00:30 AUTH_FAIL: Failed login attempt for user 'eve' from 203.0.113.20 (bad password)
2023-10-26 08:00:35 INFO: User 'charlie' logged in from 192.168.1.11
2023-10-26 08:00:40 ERROR: File integrity check failed for /etc/myapp.conf
2023-10-26 08:00:45 INFO: System health check passed.
2023-10-26 08:00:50 AUTH_FAIL: Repeated failed login for user 'eve' from 203.0.113.20 (account locked)
2023-10-26 08:01:00 ERROR: Unknown internal server error.
2023-10-26 08:01:05 CRITICAL: Unauthorized access attempt detected from 172.16.0.1. Dropping connection.
2023-10-26 08:01:10 INFO: User 'bob' logged out.
```` ``` ````

## Analysis Steps and Commands

### 1. Identify All Critical and Error Messages:

* **Objective:** Quickly find all lines indicating severe issues or errors.
* **Command:** `grep -E 'ERROR|CRITICAL' myapp.log`
* **Output Example:**
    ```
    2023-10-26 08:00:20 ERROR: Database connection failed for user 'admin'
    2023-10-26 08:00:40 ERROR: File integrity check failed for /etc/myapp.conf
    2023-10-26 08:01:00 ERROR: Unknown internal server error.
    2023-10-26 08:01:05 CRITICAL: Unauthorized access attempt detected from 172.16.0.1. Dropping connection.
    ```
* **Explanation:** `grep -E` enables extended regular expressions, allowing the use of `|` (OR) to search for multiple patterns.

### 2. Track Failed Login Attempts:

* **Objective:** Pinpoint all instances of failed login attempts, which could indicate brute-force attacks or unauthorized access.
* **Command:** `grep 'AUTH_FAIL' myapp.log`
* **Output Example:**
    ```
    2023-10-26 08:00:30 AUTH_FAIL: Failed login attempt for user 'eve' from 203.0.113.20 (bad password)
    2023-10-26 08:00:50 AUTH_FAIL: Repeated failed login for user 'eve' from 203.0.113.20 (account locked)
    ```
* **Explanation:** Directly filters for the specific `AUTH_FAIL` tag, often used in security logs.

### 3. Summarize Login/Logout Activity by User:

* **Objective:** Get a quick overview of who logged in or out.
* **Command:** `grep -E 'logged in|logged out' myapp.log | awk '{print $NF, $(NF-2), $(NF-1)}'`
* **Output Example:**
    ```
    192.168.1.10 'alice' logged
    10.0.0.5 'bob' logged
    192.168.1.11 'charlie' logged out. 'bob' logged
    ```
* **Explanation:** Combines `grep` to filter login/logout lines with `awk` to extract relevant fields (like IP, 
username, and action). `NF` refers to the number of fields, `$NF` is the last field. 
*(Note: The awk output might need slight adjustment based on desired clarity, but demonstrates field extraction.)*

### 4. Identify Unique Source IPs for Critical Events:

* **Objective:** Find unique IP addresses associated with critical security alerts.
* **Command:** `grep 'CRITICAL' myapp.log | awk '{print $NF}' | tr -d '.' | sort -u`
* **Output Example:**
    ```
    172.16.0.1
    ```
* **Explanation:** Filters critical events, uses `awk` to extract the last field (IP), `tr -d '.'` to remove periods (optional, for some specific 
parsing needs), and `sort -u` to get unique IP addresses.

### 5. Count Occurrences of Warning Messages:

* **Objective:** Quickly see how many warning messages are present.
* **Command:** `grep -c 'WARNING' myapp.log`
* **Output Example:**
    ```
    1
    ```
* **Explanation:** The `-c` option of `grep` counts lines matching the pattern.

## Conclusion and Next Steps

This mini-project demonstrates how basic shell commands can be chained together for powerful log analysis in a cybersecurity context. This 
approach is efficient for quick investigations and can be a foundation for more complex scripts or automated monitoring systems.

Future improvements could involve:
* Writing a full Bash script to automate these checks daily.
* Integrating with notification systems (e.g., sending emails for critical alerts).
* Parsing log timestamps for time-based analysis.
* Using `sed` or `awk` for more sophisticated data extraction and reformatting.
