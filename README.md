# Databrick
-Explanation of %fs in Databricks
-The %fs magic command in Databricks is used to interact with the Databricks File System (DBFS). It provides a simple way to perform file system operations such as listing, creating, or deleting directories and files. %fs is a shorthand for File System operations.

Common %fs Commands
List Files
Command: %fs ls <path>
Explanation: Lists the files and subdirectories at the specified path.
Example:
%fs ls /FileStore
Lists all files and folders in the /FileStore directory.
Create Directory
Command: %fs mkdirs <path>
Explanation: Creates a new directory at the specified path.
Example:
%fs mkdirs /FileStore/my-directory
Creates a new folder called my-directory inside /FileStore.
Remove File or Directory
Command: %fs rm <path> [recurse=True]

Explanation: Deletes the file or directory at the specified path. Use recurse=True to delete directories and their contents.

Example:

%fs rm /FileStore/my-directory/old-file.txt
Deletes the file old-file.txt from /FileStore/my-directory.

%fs rm /FileStore/my-directory/ --recurse=True
Deletes the entire directory and its contents.

Display File Content
Command: %fs head <path>
Explanation: Displays the first few bytes of a file.
Example:
%fs head /FileStore/data/sample.txt
Displays the first few lines of sample.txt.
Copy Files
Command: %fs cp <source> <destination>
Explanation: Copies files or directories from one location to another.
Example:
%fs cp /FileStore/source.txt /FileStore/destination.txt
Copies source.txt to destination.txt.
Move Files
Command: %fs mv <source> <destination>
Explanation: Moves files or directories from one location to another.
Example:
%fs mv /FileStore/source.txt /FileStore/archive/source.txt
Moves source.txt to the archive directory.
Key Advantages of %fs
Ease of Use: Designed for quick file system interactions in a Databricks notebook.
Readability: Easy to understand and use for basic file operations.
Integration: Works seamlessly with the Databricks File System (DBFS), allowing efficient management of data.
Use Case Example
# List files in a directory
%fs ls /FileStore/data/

# Create a new directory
%fs mkdirs /FileStore/data/new-folder/

# Remove a file
%fs rm /FileStore/data/sample.csv

# Copy a file
%fs cp /FileStore/data/sample.csv /FileStore/data/backup/sample.csv

# Display file content
%fs head /FileStore/data/sample.csv
These commands provide a straightforward way to manage your file system directly within Databricks notebooks!
** Using %fs commands:### **
%fs mkdirs /FileStore/tables/db2025batch
%fs mkdirs /FileStore/tables/db2025batch/bronze_layer
%fs mkdirs /FileStore/tables/db2025batch/silver_layer
%fs mkdirs /FileStore/tables/db2025batch/gold_layer
**# If you prefer to use Python to create all directories in a single cell, you can use the dbutils.fs.mkdirs method:### **
dbutils.fs.mkdirs('/FileStore/tables/db2025batch')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/bronze_layer')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/silver_layer')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/gold_layer')
**This approach is cleaner and allows you to manage all directory creation in one cell.### **
The error you're encountering (UsageError: Line magic function %fs not found) is happening because %fs is not supported in non-notebook environments. If you are working in a Databricks notebook, you can use %fs directly. If you're using a Python or Scala notebook, the syntax would be correct, but ensure you're using a notebook cell to run this magic command.

Ensure you're in a Databricks notebook and then try: bash Copy code

** This will list the contents of the db2025batch folder
** %fs ls /FileStore/tables/db2025batch
If %fs is still not working: In case %fs still doesn’t work, or you are trying it in a script or other environment, you can use dbutils as an alternative in a Python notebook:

** This will list the contents of the db2025batch folder using dbutils
dbutils.fs.ls("/FileStore/tables/db2025batch")

** Summary:
If you are in a Databricks notebook, %fs should work as expected. For Python notebooks (if %fs doesn't work), use dbutils.fs.ls() to list the contents.
