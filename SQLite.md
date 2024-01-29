# SQLite

## Debugging SQLite 

Debugging databases is an essential step in correctly implementing and developing any application that stores or manipulates data. It is crucial to ensure that the database performs optimally and provides the desired functionality to the users. In this regard, debugging SQLite databases can be a tricky task, as it depends on several factors such as the environment, hardware, and software used. 

This report focuses the findings on an attempt to debug SQLite databases in an Android environment, particularly when using the Ionic SQLite plugin. The primary objective is to address the challenges encountered when inspecting the database for debugging or data analysis. The Ionic SQLite plugin is a popular plugin used for interacting with SQLite databases in Ionic applications. However, these databases require device hardware and are not supported by browsers, making it particularly challenging to inspect the database without the correct tools. To address this challenge, this paper proposes a method for debugging SQLite databases in an Android environment.

Using Android Debug Bridge (ADB), which allows developers to communicate with an Android device from a computer and will enable to to proceed with finding a solution to debug SQLite databases. The ADB tool provides a command-line interface that enables developers to execute commands on an Android device, such as copying files to the device, installing and uninstalling applications, and accessing the device's file system.  

Issue reference: https://stackoverflow.com/questions/65058335/android-studio-database-inspector-always-showing-database-as-closed

### Attempts 

While conducting research, I made multiple attempts to gather and inspect the database from an Android device. After reading a few online forums, I learned that the recommended solution was to move the database to an extractable directory, and then extract it to a local directory using adb shell commands like `-adb -d shell "run-as APPLICATION_NAME cat ./databases/DATABASE_NAME.db" > database.db` and then pulling the file using the pull command `adb pull`. However, this solution wasn't reliable due to the permissions of the files. 

After investigating the permissions and how they worked, I discovered that they were similar to the Linux operating system and how Linux permissions work. Using my previous knowledge, I attempted to change the permissions of the directory and files using similar commands to `chmod -R 777 /data/data/APPLICATION_NAME/databases` (these permission changes were only applied to a local device and did not pose a security risk). Despite these changes, I continued to receive a "Permission denied" error, meaning that this was not the correct way to gain access to the database files on an Android device.

Upon conducting an in-depth investigation, I also explored a coding solution that was proposed on the Ionic forums. The solution advised dumping out the database either in the inspector's console or within Logcast on Android Studio. However, I encountered a significant roadblock as the dumped database was still encrypted. Deciphering the database would have taken an excessive amount of time and effort, which led me to conclude that this solution was not feasible.

### Solution 

After finidng a proposed solution which entailed going through the device as root for extracting the database file using the following commands:

```
-	adb root        
-	adb shell
-	su
-	cd data/data/com.cgs.premiertsworkmate/databases 
-	pull DATABASE_NAME.db path/to/local/dir
```
With my previous experience with Linux, I realized that I didn't have an account on the device. I tried opening up the permissions to any account, except for root. Although root would have super admin access without any restrictions, I hadn't set a password for it, which could be dangerous if used for any live or open device. After some careful consideration, I decided to use root to access and pull the files. Although it was risky, it was the only viable option. Finally, after some effort, the files were successfully retrieved. However, this was just the beginning. It was like taking the results out of the frying pan and throwing them right into the fire.

After analyzing the extracted database file, we encountered a major issue where the database was encrypted, which led us to withdraw our successful solution claims and look for alternative methods to solve this problem. Upon further inspection, we noticed that a single salt or decrypted key was not defined, and the file type was `.db`, which required a `.sql` file for insertion into a SQL environment. To overcome this hurdle, we used the `sqlite3` CLI tool to convert the documents, which successfully decrypted the file for us. However, it should be noted that the tool used the wrong syntax, such as single quotes `'` instead of backticks '`', which can cause some SQL tools to malfunction, especially SQLYog and PHPMyAdmin.

We resolved this issue by converting the documents using the following command:

```
sqlite3 DATABASE_NAME.db .dump > exportDB.sql
```

After inserting the converted documents into the database, we were able to successfully inspect the data and the database. These findings provide valuable insights into the challenges faced during the research process and highlight the importance of leveraging appropriate tools and techniques to overcome such obstacles.

### Conclusion 

After conducting extensive research and analysis, it is clear that there are remarkable similarities between the Linux operating system and Android's operating system. Through this research, it was discovered that Samsung devices use Linux versions of their kernels, which explains the similarities between the CLI commands and processing involved in both systems. This newfound knowledge has shed further light on how Android systems work.

As a result of this research, we have developed a quick and effective solution to address the issue of SQLite database debugging. This solution has the potential to revolutionize the way developers approach debugging, and could significantly improve the efficiency and accuracy of the process.

Overall, this research has not only provided a valuable solution to a pressing issue, but has also deepened our understanding of the underlying principles of operating systems and software development. We believe that these findings will have a significant impact on the field of computer science and will pave the way for further innovation and advancement in the years to come.

### Additional Information 

Refernece: 

- [2024] https://stackoverflow.com/questions/65058335/android-studio-database-inspector-always-showing-database-as-closed - Closer look at the main issue related to this report around inspecting SQLite databases.
- [2024] https://forum.ionicframework.com/t/prepopulated-sqlite-databases-in-ionic/6558/20 - example forum research.
- [2024] https://eu.community.samsung.com/t5/tablets/linux-device-masquerading-as-galaxy-tab-a/td-p/4473805 - Samsung forums detailing similarities between linux and Android
