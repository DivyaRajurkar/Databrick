

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
