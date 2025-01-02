

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

- `%fs` commands are for managing files and directories in Databricks notebooks.  The `dbutils` module is a utility library provided by Databricks for managing files, secrets, jobs, widgets, and other tasks. Below is a comprehensive list of important `dbutils` commands categorized by their functions:

---

### **1. File System Operations (`dbutils.fs`)**
Used to interact with the Databricks File System (DBFS).

- **`dbutils.fs.ls(path)`**: Lists files in the given path.
- **`dbutils.fs.mkdirs(path)`**: Creates directories at the specified path.
- **`dbutils.fs.rm(path, recurse)`**: Removes files or directories. Use `recurse=True` for recursive deletion.
- **`dbutils.fs.cp(source, destination, recurse)`**: Copies files from the source to the destination. Use `recurse=True` for recursive copying.
- **`dbutils.fs.mv(source, destination)`**: Moves files from the source to the destination.
- **`dbutils.fs.head(path, max_bytes)`**: Displays the first few bytes of a file (default 65536 bytes).
- **`dbutils.fs.put(path, contents, overwrite)`**: Creates or overwrites a file with the given contents.

---

### **2. Secrets Management (`dbutils.secrets`)**
Used to manage secrets securely.

- **`dbutils.secrets.list(scope)`**: Lists all secrets in the given scope.
- **`dbutils.secrets.listScopes()`**: Lists all available secret scopes.
- **`dbutils.secrets.get(scope, key)`**: Retrieves the value of a secret for the given key in the specified scope.
- **`dbutils.secrets.getBytes(scope, key)`**: Retrieves a secret value as bytes.

---

### **3. Widgets for Parameterization (`dbutils.widgets`)**
Used to create, manage, and retrieve widgets for notebooks.

- **`dbutils.widgets.text(name, default, label)`**: Creates a text input widget.
- **`dbutils.widgets.dropdown(name, default, choices, label)`**: Creates a dropdown widget.
- **`dbutils.widgets.combobox(name, default, choices, label)`**: Creates a combobox widget.
- **`dbutils.widgets.multiselect(name, default, choices, label)`**: Creates a multiselect widget.
- **`dbutils.widgets.remove(name)`**: Removes a specific widget.
- **`dbutils.widgets.removeAll()`**: Removes all widgets.
- **`dbutils.widgets.get(name)`**: Retrieves the current value of a widget.

---

### **4. Notebook Utilities (`dbutils.notebook`)**
Used for chaining and running notebooks.

- **`dbutils.notebook.run(notebook_path, timeout_seconds, arguments)`**: Runs a notebook and returns its output.
- **`dbutils.notebook.exit(value)`**: Exits the current notebook with the given value.

---

### **5. Jobs Utilities (`dbutils.jobs`)**
Used for interacting with jobs in Databricks.

- **`dbutils.jobs.taskValues.set(key, value)`**: Sets a key-value pair for task values.
- **`dbutils.jobs.taskValues.get(key, default)`**: Retrieves the value of a specified key for task values.
- **`dbutils.jobs.taskValues.getAll()`**: Retrieves all task values.

---

### **6. Utilities Information (`dbutils.library`)**
Used to manage libraries.

- **`dbutils.library.install(library_name)`**: Installs a library.
- **`dbutils.library.installPyPI(package, repo, extras)`**: Installs a Python package from PyPI.
- **`dbutils.library.restartPython()`**: Restarts the Python process for library changes.
- **`dbutils.library.list()`**: Lists all installed libraries.

---

### **7. Utilities Versioning (`dbutils`)**
Used to retrieve the version of `dbutils`.

- **`dbutils.help()`**: Displays help for `dbutils`.
- **`dbutils.fs.help()`**: Displays help for filesystem utilities.
- **`dbutils.secrets.help()`**: Displays help for sHere’s a detailed explanation of some commonly used `dbutils` commands with examples:

---

### **1. File System Operations (`dbutils.fs`)**

#### **Command: `dbutils.fs.ls(path)`**
Lists files and directories in the given path.

**Example:**
```python
files = dbutils.fs.ls("/databricks-datasets")
for file in files:
    print(file.name)
```
**Explanation:**
- Lists all files and directories in the `/databricks-datasets` folder.
- Prints the name of each file or folder.

---

#### **Command: `dbutils.fs.put(path, contents, overwrite)`**
Creates or overwrites a file with the specified content.

**Example:**
```python
dbutils.fs.put("/tmp/sample.txt", "Hello, Databricks!", overwrite=True)
```
**Explanation:**
- Creates a file named `sample.txt` in the `/tmp` directory with the content `Hello, Databricks!`.
- The `overwrite=True` parameter allows overwriting the file if it already exists.

---

#### **Command: `dbutils.fs.rm(path, recurse)`**
Removes files or directories.

**Example:**
```python
dbutils.fs.rm("/tmp/sample.txt", recurse=False)
```
**Explanation:**
- Deletes the `sample.txt` file from the `/tmp` directory.
- The `recurse` parameter is set to `False` to ensure non-recursive deletion.

---

### **2. Secrets Management (`dbutils.secrets`)**

#### **Command: `dbutils.secrets.get(scope, key)`**
Retrieves the value of a secret.

**Example:**
```python
api_key = dbutils.secrets.get(scope="my-scope", key="api-key")
print(api_key)  # Avoid printing sensitive information in production
```
**Explanation:**
- Fetches the value of the secret `api-key` from the secret scope `my-scope`.
- Useful for securely accessing sensitive information like API keys or credentials.

---

### **3. Widgets for Parameterization (`dbutils.widgets`)**

#### **Command: `dbutils.widgets.text(name, default, label)`**
Creates a text input widget.

**Example:**
```python
dbutils.widgets.text("username", "default_user", "Enter your username")
username = dbutils.widgets.get("username")
print(f"Username: {username}")
```
**Explanation:**
- Creates a widget named `username` with a default value of `default_user`.
- The user can input a custom value, and the script retrieves it using `dbutils.widgets.get()`.

---

#### **Command: `dbutils.widgets.remove(name)`**
Removes a specific widget.

**Example:**
```python
dbutils.widgets.remove("username")
```
**Explanation:**
- Removes the widget named `username`.
- Useful for cleaning up widgets after use.

---

### **4. Notebook Utilities (`dbutils.notebook`)**

#### **Command: `dbutils.notebook.run()`**
Runs another notebook.

**Example:**
```python
result = dbutils.notebook.run("/Users/username/other_notebook", 60, {"param1": "value1"})
print(result)
```
**Explanation:**
- Runs the notebook located at `/Users/username/other_notebook` with a timeout of 60 seconds.
- Passes `param1` with the value `value1` as an argument to the notebook.
- Returns the result of the notebook execution.

---

### **5. Jobs Utilities (`dbutils.jobs`)**

#### **Command: `dbutils.jobs.taskValues.set(key, value)`**
Stores task-specific values.

**Example:**
```python
dbutils.jobs.taskValues.set("output_path", "/tmp/output")
```
**Explanation:**
- Saves the value `/tmp/output` under the key `output_path`.
- Task values can be retrieved by downstream tasks in a multi-task job.

#### **Command: `dbutils.jobs.taskValues.get(key, default)`**
Retrieves task-specific values.

**Example:**
```python
output_path = dbutils.jobs.taskValues.get("output_path", "/default/path")
print(output_path)
```
**Explanation:**
- Retrieves the value stored under `output_path`.
- If the key doesn’t exist, it returns `/default/path`.

---

### **6. Utilities Versioning (`dbutils.help`)**

#### **Command: `dbutils.help()`**
Displays help for `dbutils`.

**Example:**
```python
dbutils.help()
```
**Explanation:**
- Displays a list of all available `dbutils` commands and their descriptions.
- Useful for discovering new commands and their usage.

---

Let me know which command you’d like to explore further!ecret utilities.

---

These commands cover most common use cases in Databricks workflows. Let me know if you'd like examples or specific scenarios for using any of these commands!
- If using Python notebooks and `%fs` doesn't work, use `dbutils.fs` commands.  
```



This version flows continuously without separate sections while maintaining clarity and readability. Let me know if you'd like further refinements!
