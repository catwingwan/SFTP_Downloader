-- SFTP Downloader Script Explanation

Overview
--------
This Python script provides a robust SFTP file downloader with military-grade reliability features. It's designed to handle unstable network connections, resume interrupted transfers, and optimize download performance.


Key Features
------------
o Chunked transfer protocol - Downloads files in 2MB chunks for better reliability
o Automatic resume - Can restart downloads from the exact breakpoint if interrupted
o Connection stability - Implements aggressive keepalives and TCP optimizations
o Progressive retry logic - 7 retry attempts with increasing delays (5s to 10m)
o Cross-platform support - Works on Linux, macOS, and Windows
o File tracking - Records last downloaded file to only get newer files
o Server sync - Copies downloaded files to a server directory


Configuration
-------------
The script uses environment variables for configuration (loaded from a .env file):

Variable				Description
SFTP_HOST				SFTP server hostname/IP
SFTP_PORT				SFTP server port
SFTP_USER				SFTP username
SFTP_PASS				SFTP password
SFTP_DIR				Remote directory path on SFTP server
LOCAL_DIR				Local directory to save downloaded files
SERVER_DIR				Additional directory to sync files to
LOG_FILE				Path to log file
LAST_FILE_RECORD		File to track last downloaded filename


Technical Details
-----------------
* Uses Paramiko library for SFTP operations
* Implements TCP keepalive options (OS-specific)
* Compression enabled for transfers
* Large window size (16MB) and rekey settings (512MB)
* 128KB buffer size for efficient transfers
* Comprehensive logging to file and console


Error Handling
--------------
* Connection watchdog verifies active connection
* 7 retry attempts with exponential backoff
* Final file size verification
* Clean connection teardown


File Selection Logic
--------------------
* Only downloads files containing 'IPI' in filename
* Filters files based on date extracted from filename
* Tracks last downloaded file to only get newer files
