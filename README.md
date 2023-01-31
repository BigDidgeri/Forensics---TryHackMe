# Forensics---TryHackMe #
## Task 1 - Volatility Forensics ##
### What is the Operating System of this Dump file? (OS name) ###
By running the ```imageinfo``` plugin on volatility we can identify that the operating system is running ```windows```
![image](https://user-images.githubusercontent.com/18509521/215691233-131e108f-c7a2-40c7-9b02-54a6f9d5378a.png)

### What is the PID of SearchIndexer? ###
```2180``` Run the pstree plugin to get a list of all running process that are present
![image](https://user-images.githubusercontent.com/18509521/215691472-6eb7851e-6937-4c40-8dca-2775d5902b0f.png)

### What is the last directory accessed by the user? (The last folder name as it is?) ###
ShellBags contain details about a user's viewed folders, using the shellbags plugin we can get a list of all the files and directories the user has accessed. After some searching for the latest entry I am able to identify ```deleted_files``` as the last accessed directory/
![image](https://user-images.githubusercontent.com/18509521/215700002-8192ff19-7c40-487d-8bdf-9d9d73aa62e2.png)

## Task 2 - Task2 ##
##There are many suspicious open ports; which one is it? (ANSWER format: protocol:port)##
