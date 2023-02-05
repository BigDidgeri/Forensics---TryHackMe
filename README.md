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
### There are many suspicious open ports; which one is it? (ANSWER format: protocol:port) ###
```UDP:5005```
![image](https://user-images.githubusercontent.com/18509521/215964632-fbff4bed-324f-40cc-808e-3ad7eeaf1fba.png)

### Vads tag and execute protection are strong indicators of malicious processes; can you find which they are? (ANSWER format: Pid1;Pid2;Pid3) ###
Here we can run the malfind command to find the processes that are being identified as suspicious. 
![image](https://user-images.githubusercontent.com/18509521/216006733-3104585c-a299-403b-9781-94ffebc12893.png)
```1820;1860;2464```

## Task 3 - IOC SAGA ##
### 'www.go****.ru' (write full url without any quotation marks) ###
To start off we are going to need tu dump the processes so we can query what is inside of them. This can be done by using the memdump plugin ``` vol2 -f victim.raw --profile=Win7SP1x64 memdump -p 1820 --dump-dir dumps/ ``` We will do this with all three processes.
![image](https://user-images.githubusercontent.com/18509521/216812475-374174e1-9152-4337-a993-0774b03014f7.png)
Now we will run strings on the processes and concatenate them into a txt file to make querying easier.
![image](https://user-images.githubusercontent.com/18509521/216812534-1db3ce19-6c93-436a-b288-e1c1a0b49444.png)
'www.go****.ru' Is the URL we have to find, as they have given us the length of it we can use the ```.``` wildcard to search for the exact url. We will use the command ```grep -i 'www.\go....\.ru' strings.txt``` which will search our strings file for a string starting with www. and containing exactly for wildcard positions (the go....) and then finally ending in ru.
![image](https://user-images.githubusercontent.com/18509521/216813219-d64d6f23-d252-46a4-9923-ee7820613238.png)
The flag is ```www.goporn.ru```

### 'www.i****.com' (write full url without any quotation marks) ###
Same process as above
![image](https://user-images.githubusercontent.com/18509521/216813303-fd027dc6-7a2b-4719-a8fc-f5a58df4e714.png)
Flag is ```www.ikaka.com```

### 'www.ic******.com' ###
Same process as above
![image](https://user-images.githubusercontent.com/18509521/216813331-7f9b9d38-4baa-4461-b6aa-316945d7b0d7.png)
Flag is ```www.icsalabs.com```

### 202.***.233.*** (Write full IP) ###
We will need to change the regex but can practically do the same thing for this task we will use ``` grep '202\....\.233\....' strings.txt ```
![image](https://user-images.githubusercontent.com/18509521/216813710-13d222b9-5184-475c-94cf-843810dc935c.png)
The flag is ```202.107.233.211```

### ***.200.**.164 (Write full IP) ###
Do the same as above just rearrange where necessary.
![image](https://user-images.githubusercontent.com/18509521/216813797-939f6fb2-b381-4a2b-ae60-904cccba68d1.png)
The flag is ```209.200.12.164```

### 209.190.***.*** ###
Same as above
![image](https://user-images.githubusercontent.com/18509521/216813850-a905c87f-94ac-44ae-8e8e-04f90b31c28e.png)
The flag is ```209.190.122.186```

### What is the unique environmental variable of PID 2464? ###
For this challenge we will use the envars plugin to get the environment variables for pid 2464
![image](https://user-images.githubusercontent.com/18509521/216814007-0fba7815-eab7-47d0-926a-e7d64c1c2110.png)
The flag is ```OANOCACHE```
