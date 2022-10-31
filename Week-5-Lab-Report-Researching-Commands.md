# Week 5 Lab Report - Researching Commands
## "Find" command

---

**!!! Assumming that: the current working directory is ./technical for all codes below.**

### 1. -name option - Finding Files by Name

```
  $ find . -name chapter-1.txt
```
	
   Output: 
   ```
   ./911report/chapter-1.txt
   ```
	 
   This command will find all the files that have the name "chapter-1.txt" in the current working directory (be shown "."). This directory can be changed to anywhere you want.
   For example, if you want to find a file starting with the string "pmed.002027" in name in the file "plos", you can run this command below.
   ```
   $ find ./plos -name pmed.002027*.txt
   ```
   Output:
   
   ```
   ./plos/pmed.0020273.txt
   ./plos/pmed.0020272.txt
   ./plos/pmed.0020275.txt
   ./plos/pmed.0020274.txt
   ./plos/pmed.0020278.txt
   ```
   
   Or if you don't remember exactly file name (uppercase or lowercase), you can use **-iname** option instead.
   
   ```
   $ find ./government/Media -iname farm_workers.txt
   ```
	
   Output: 
   
   ```
   ./government/Media/Farm_workers.txt
   ```

### 2. -type option - Finding Files by Type

* **-type d**: for directories
	
	To find all directories in the current dir, run this command:
	
	```
	$ find . -type d
	```
	
   Output: 
   ```
   .
   ./government
   ./government/About_LSC
   ./government/Env_Prot_Agen
   ./government/Alcohol_Problems
   ./government/Gen_Account_Office
   ./government/Post_Rate_Comm
   ./government/Media
   ./plos
   ./biomed
   ./911report
   ```
	
   If you want to find a directory with the name "Media", run this command: 
   
   ```
   $ find . -type d -name Media
   ```
	 
   Or this one if you don't remember exactly dir name, run this one:
   
   ```
   $ find . -type d -iname media
   ```
	
   Output:
   
   ```
   ./government/Media
   ```
	 
* **-type f**: for files
	
   If you want to find a file starting with "tech" in name, you can try this command.
   
   ```
   $ find . -type f -name tech*.txt
   ```
	
   Output:
   
   ```
   ./government/Env_Prot_Agen/tech_sectiong.txt
   ./government/Env_Prot_Agen/tech_adden.txt
   ```

### 3. -depth - Finding files by depth 

* We have the current dir and its sub dir like below:
	
  ![image](https://user-images.githubusercontent.com/114208205/198870569-b5822922-d750-45a3-bf36-1b3e2f1d07ea.png)

* **-maxdepth n**: Find the file under the current directory and n level down.

	To file a file "rr74.txt" have path `./biomed/rr74.txt` with 
	
	- Maxdepth = 2
	
	```
	$ find . -maxdepth 2 -name rr74.txt
	```
	
	Output:
	
	```
	./biomed/rr74.txt
	```
	
	- Maxdepth = 1
	
	```
	$ find . -maxdepth 1 -name rr74.txt
	```
	
	Output: nothing bc the file "rr74.tzt" has level 2 from the current dir and maxdepth is 1 (find in depth 1 and 0(current dir))
	
* **-mindepth n**: Find the file under the current directory and n level up.

	To find a file "rr74.txt" has the path `./biomed/rr74.txt` with
	- Mindepth = 0
	
	```
	$ find .  -name rr74.txt
	```

	Output:
	
	```
	./biomed/rr74.txt
	```

	- Mindepth = 3 
	
	```
	find . -mindepth 3 -name rr74.txt
	```
	
	Output: Nothing bc the file "rr74.tzt" has level 2 from the current dir and mindepth is 3 (find in depth 3 and up)
	
* To find a file "bill.txt" (depth 3) has the path `./government/Env_Prot_Agen/bill.txt` in depth from 1 to 3
	
	```
	$ find . -mindepth 1 -maxdepth 3 -name bill.txt
	```
	
	Output: 
	
	```
	./government/Env_Prot_Agen/bill.txt
	```

	




