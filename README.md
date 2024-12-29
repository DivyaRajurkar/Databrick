

```markdown
# Databricks  

The `%fs` magic command in Databricks is used to interact with the Databricks File System (DBFS). It provides an easy way to perform file system operations like listing, creating, or deleting directories and files. `%fs` is shorthand for File System operations.  

### Common `%fs` Commands  

1. **List Files**:  
   Command: `%fs ls <path>`  
   Example:  
   ```bash
   %fs ls /FileStore
   ```  
   Lists all files and folders in the `/FileStore` directory.  

2. **Create Directory**:  
   Command: `%fs mkdirs <path>`  
   Example:  
   ```bash
   %fs mkdirs /FileStore/my-directory
   ```  
   Creates a new directory named `my-directory` inside `/FileStore`.  

3. **Remove File or Directory**:  
   Command: `%fs rm <path> [recurse=True]`  
   Examples:  
   ```bash
   %fs rm /FileStore/my-directory/old-file.txt
   ```  
   Deletes the file `old-file.txt` from `/FileStore/my-directory`.  

   ```bash
   %fs rm /FileStore/my-directory/ --recurse=True
   ```  
   Deletes the directory `my-directory` and its contents.  

4. **Display File Content**:  
   Command: `%fs head <path>`  
   Example:  
   ```bash
   %fs head /FileStore/data/sample.txt
   ```  
   Displays the first few lines of `sample.txt`.  

5. **Copy Files**:  
   Command: `%fs cp <source> <destination>`  
   Example:  
   ```bash
   %fs cp /FileStore/source.txt /FileStore/destination.txt
   ```  
   Copies `source.txt` to `destination.txt`.  

6. **Move Files**:  
   Command: `%fs mv <source> <destination>`  
   Example:  
   ```bash
   %fs mv /FileStore/source.txt /FileStore/archive/source.txt
   ```  
   Moves `source.txt` to the `archive` directory.  

### Use Case Examples  

- List files in a directory:  
  ```bash
  %fs ls /FileStore/data/
  ```  

- Create a new directory:  
  ```bash
  %fs mkdirs /FileStore/data/new-folder/
  ```  

- Remove a file:  
  ```bash
  %fs rm /FileStore/data/sample.csv
  ```  

- Copy a file:  
  ```bash
  %fs cp /FileStore/data/sample.csv /FileStore/data/backup/sample.csv
  ```  

- Display file content:  
  ```bash
  %fs head /FileStore/data/sample.csv
  ```  

### Using `%fs` Commands to Create Directories  

```bash
%fs mkdirs /FileStore/tables/db2025batch
%fs mkdirs /FileStore/tables/db2025batch/bronze_layer
%fs mkdirs /FileStore/tables/db2025batch/silver_layer
%fs mkdirs /FileStore/tables/db2025batch/gold_layer
```  

### Using `dbutils` for Directory Creation  

If you prefer Python:  
```python
dbutils.fs.mkdirs('/FileStore/tables/db2025batch')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/bronze_layer')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/silver_layer')
dbutils.fs.mkdirs('/FileStore/tables/db2025batch/gold_layer')
```  

This approach is cleaner and allows managing all directory creation in a single cell.  
Here is the formatted content written in **GitHub README** markdown style:

```markdown
# Databricks `dbutils.fs` Operations

This document provides examples of using `dbutils.fs` commands in Databricks for various file operations such as creating directories, writing files, reading content, copying files, and handling errors.

---

## 1. Create a Directory
Use the `mkdirs` command to create a new directory.

```python
dbutils.fs.mkdirs('/FileStore/tables/db2025batch')
```

---

## 2. Write a File
Write content to a file using the `put` command.

```python
dbutils.fs.put('/FileStore/tables/db2025batch/sample.txt', "This is a sample file.")
```

---

## 3. Read the File
Read the content of a file using the `head` command.

```python
content = dbutils.fs.head('/FileStore/tables/db2025batch/sample.txt')
print("File Content:", content)
```

---

## 4. Copy the File
Copy a file from one location to another using the `cp` command.

```python
# Create a backup directory
dbutils.fs.mkdirs('/FileStore/tables/backup')

# Copy the file
dbutils.fs.cp('/FileStore/tables/db2025batch/sample.txt', '/FileStore/tables/backup/sample_copy.txt')
```

---

## 5. Remove the Original File
Remove a file using the `rm` command.

```python
dbutils.fs.rm('/FileStore/tables/db2025batch/sample.txt')
```

---

## 6. Remove the Directory
Delete directories and their contents recursively.

```python
dbutils.fs.rm('/FileStore/tables/db2025batch', True)
dbutils.fs.rm('/FileStore/tables/backup', True)
print("Cleanup completed!")
```

---

## Reading Files with `head`

### 1. Writing a Sample File
Before using the `head` command, create a sample file:

```python
dbutils.fs.put("/FileStore/tables/example.txt", "Hello, Databricks! Welcome to file handling using dbutils.")
print("File written successfully!")
```

---

### 2. Reading File Content with `head`
Use the `head` command to read the file content:

```python
content = dbutils.fs.head("/FileStore/tables/example.txt")
print("File Content:", content)
```

**Output:**
```
File Content: Hello, Databricks! Welcome to file handling using dbutils.
```

---

### 3. Reading Only the First Few Characters
You can limit the number of characters read using the `maxBytes` parameter:

```python
content = dbutils.fs.head("/FileStore/tables/example.txt", maxBytes=20)
print("Partial Content:", content)
```

**Output:**
```
Partial Content: Hello, Databricks! W
```

---

## Error Handling
If the file does not exist or the path is incorrect, you’ll get an error like:

```
java.io.FileNotFoundException: File /FileStore/tables/nonexistent.txt does not exist.
```

### Handling Missing Files
Use a `try-except` block to handle missing files gracefully:

```python
try:
    content = dbutils.fs.head("/FileStore/tables/nonexistent.txt")
    print("File Content:", content)
except Exception as e:
    print("Error:", str(e))
```

This ensures smooth execution and handles missing file scenarios effectively.
``` 

This README-styled format is well-organized for GitHub and suitable for documenting your `dbutils.fs` operations.

### Handling Errors  

If you encounter the error `UsageError: Line magic function %fs not found`, ensure you are in a Databricks notebook.  

- To list folder contents in Databricks:  
  ```bash
  %fs ls /FileStore/tables/db2025batch
  ```  

- If `%fs` doesn't work, use `dbutils` as an alternative:  
  ```python
  dbutils.fs.ls("/FileStore/tables/db2025batch")
  ```  

### Summary  

- `%fs` commands are for managing files and directories in Databricks notebooks.  
- If using Python notebooks and `%fs` doesn't work, use `dbutils.fs` commands.  
```  

This version flows continuously without separate sections while maintaining clarity and readability. Let me know if you'd like further refinements!
