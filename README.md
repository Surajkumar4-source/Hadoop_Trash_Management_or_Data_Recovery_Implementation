
# Managing Trash in Hadoop


The Trash feature in Hadoop's HDFS provides a safety mechanism to prevent accidental data loss by temporarily moving deleted files to a designated Trash directory rather than deleting them immediately. This functionality allows users to recover files within a specified retention period, adding a layer of data protection to the Hadoop environment.

## Key Benefits of Trash in Hadoop
- **Accidental Deletion Prevention: Trash allows for the recovery of files mistakenly deleted by the hdfs dfs -rm command, minimizing data loss risks.**
- **Configurable Retention: The Trash interval can be adjusted to control how long deleted files remain recoverable.**
- **Ease of Recovery: With files accessible in the Trash directory, users can quickly restore deleted files to their original location or a new path.**



## Enabling and Configuring Trash

The Trash feature is enabled by default in HDFS, but you can configure its behavior in the `core-site.xml` file. Here are key properties you can set:

### Trash Interval
Defines how long files remain in Trash before being permanently deleted. The interval is set in minutes.

```xml
<property>
    <name>fs.trash.interval</name>
    <value>1440</value> <!-- e.g., 1440 minutes (24 hours) -->
</property>
```
**After this restart the namenode**

## Example Commands

### 1. Delete a File (Moves to Trash)

```bash
hdfs dfs -rm /demo/acts2.txt
# Output: 2024-10-26 02:47:08,735 INFO fs.TrashPolicyDefault: Moved: 'hdfs://manager:9000/demo/acts2.txt' to trash at: hdfs://manager:9000/user/hduser/.Trash/Current/demo/acts2.txt
```

### 2. List Files After Deletion

```bash
hdfs dfs -ls /demo
# Output: Found 4 items (includes remaining files)
```

### 3. Check Current Trash Directory:

**The Trash directory is located in the HDFS path /user/<username>/.Trash/.
You can list the contents of the Trash directory using the following command:
Replace <username> with your actual HDFS username.**

```bash
hdfs dfs -ls /user/<username>/.Trash/Current/

Eg.-in my case ---   hdfs dfs -ls /user/hduser/.Trash
# Output: Found 2 items
# drwx------   - hduser supergroup          0 2024-10-26 02:37 /user/hduser/.Trash/241026024000
# drwx------   - hduser supergroup          0 2024-10-26 02:47 /user/hduser/.Trash/Current
```

### 4. Locate the Deleted File: 
**Navigate to the Current directory inside your Trash to find the deleted files. Use:**

```bash
hdfs dfs -ls /user/<username>/.Trash/Current/

Eg. in my case---= hdfs dfs -ls /user/hduser/.Trash/Current
# Output: Found 1 items
# drwx------   - hduser supergroup          0 2024-10-26 02:47 /user/hduser/.Trash/Current/demo
```

### 5. Check Specific Deleted File in Current Trash

```bash
hdfs dfs -ls /user/<username>/.Trash/Current/<dir name>

eg. in my case ----- hdfs dfs -ls /user/hduser/.Trash/Current/demo
# Output: Found 1 items
# -rw-r--r--   2 hduser supergroup          9 2024-10-24 23:54 /user/hduser/.Trash/Current/demo/acts2.txt
```

### 6. Recover  a Deleted File from Current Trash:

**To recover a specific file from Trash, use the hdfs dfs -mv command to move it back to its original location or to a new location of your choice. For example:**

```bash
hdfs dfs -mv /user/<username>/.Trash/Current/yourfile.txt /path/to/recovery/location/

Eg. in my case --- hdfs dfs -mv /user/hduser/.Trash/Current/demo/acts2.txt /demo
```

### 7. Verify File Restoration Again
**After moving the file, you can verify that it has been successfully restored by listing the contents of the destination directory:**

```bash

hdfs dfs -ls /path/to/recovery/location/

Eg. in my case ---  hdfs dfs -ls /demo
# Output: Found 5 items (includes restored acts2.txt)
```

## Summary

This sequence of commands illustrates how to effectively manage files in HDFS, particularly with regard to deleting and restoring files using the Trash mechanism. The commands demonstrate listing directories, verifying contents, moving files, and ensuring proper file restoration for a user. If you have further questions or need more examples, feel free to ask!








<br>
<br>
<br>
<br>



**👨‍💻 𝓒𝓻𝓪𝓯𝓽𝓮𝓭 𝓫𝔂**: [Suraj Kumar Choudhary](https://github.com/Surajkumar4-source) | 📩 **𝓕𝓮𝓮𝓵 𝓯𝓻𝓮𝓮 𝓽𝓸 𝓓𝓜 𝓯𝓸𝓻 𝓪𝓷𝔂 𝓱𝓮𝓵𝓹**: [csuraj982@gmail.com](mailto:csuraj982@gmail.com)




<br>
