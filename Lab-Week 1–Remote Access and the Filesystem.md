# Lab-Week 1–Remote Access and the Filesystem
## How to log into a course-specific account on ieng6

---

**1. Installing VScode**

   Go to the [`Visual Studio Code website`](https://code.visualstudio.com/), and follow the instructions to download and install it on your computer.

   <img width="721" alt="Screen Shot 2022-09-29 at 11 37 54 AM" src="https://user-images.githubusercontent.com/114208205/193116539-fbbb0e80-c3a5-4aae-b5d7-affa8531d98c.png">

**2. Remotely Connecting**

   * First, open a terminal in VSCode and connect to the server ieng6: `$ ssh cs15lfa22@ieng6.ucsd.edu`

   * Use your **username** instead of `cs15lfa22`. You will be required a password to log in your CSE15L account.

     ![Screen Shot 2022-09-29 at 2 18 27 PM](https://user-images.githubusercontent.com/114208205/193174539-8e0af36d-c5c8-4416-9c1a-7e14ede672c5.png)

   * Next, enter your password *correctly*, you will get a message like this: 

     ![Screen Shot 2022-09-29 at 2 20 45 PM](https://user-images.githubusercontent.com/114208205/193175298-f6112f84-5a54-4ee9-a746-94dd88edd63b.png)


**3. Trying Some Commands**

   Try to type these commands below:

   * `cd ~` and `cd`

     <img width="236" alt="Screen Shot 2022-09-29 at 4 18 41 PM" src="https://user-images.githubusercontent.com/114208205/193175684-d7b82364-fc44-4b70-ad68-5214ca011d76.png">

   * `ls -lat`
 
     <img width="538" alt="Screen Shot 2022-09-29 at 4 18 55 PM" src="https://user-images.githubusercontent.com/114208205/193175857-fc8faa94-f869-4120-be12-d2116f48f5c1.png">

   * `ls -a`

     <img width="547" alt="Screen Shot 2022-09-29 at 4 19 14 PM" src="https://user-images.githubusercontent.com/114208205/193175972-2f842a9b-c2ee-4a7b-9649-e68744518a97.png">
     
   * `ls <directory>` where <directory> is /home/linux/ieng6/cs15lfa22/cs15lfa22abc.
      `cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/`
      `cat /home/linux/ieng6/cs15lfa22/public/hello.txt`

      Use your **username** instead of `cs15lfa22`.
 
      <img width="557" alt="Screen Shot 2022-09-29 at 4 21 06 PM" src="https://user-images.githubusercontent.com/114208205/193176254-8745b7a9-3036-466b-8f7b-5cf4f985d7eb.png">


**4. Moving Files with scp**

   * Create a file on your computer. Examlpe, I have a file named `WhereAmI.java`.
   * Change direction to the directory of the file you just created by using `$ cd <the directory of the file>`. For example, my file is saved on ~/Documents -> I will type `$cd Documents`.
   * Use the command `$ scp filename serverName: <directory>` to copy a file on your workstation to a server. 
     Run this command `$ scp WhereAmI.java cs15lfa22@ieng6.ucsd.edu:~/`  Use your **username** instead of `cs15lfa22`.
  
     <img width="573" alt="Screen Shot 2022-09-29 at 4 48 49 PM" src="https://user-images.githubusercontent.com/114208205/193184037-49b7cc5d-8fb4-417d-8de7-8794bec920ee.png">


**5. Setting an SSH Key**

   * On your computer, run this command `$ ssh-keygen` to set up the keygen. 
     I already set this up in class CSE30, so I can not attach a screenshot of instructions at this step.
   * Coppy the keygen (the public key saved in file id_rsa.pub) to the server. 
      `$ scp /Users/<username on your computer>/.ssh/id_rsa.pub cs15lfa22@ieng6.ucsd.edu:~/.ssh/authorized_keys`
     Use your **username** instead of `cs15lfa22`
   * Now, you can log in to the server ieng6 without typing the password.

     <img width="480" alt="Screen Shot 2022-09-29 at 5 25 33 PM" src="https://user-images.githubusercontent.com/114208205/193185005-fd25e657-d6cd-4812-bd8f-493b64e836f7.png">


**6. Optimizing Remote Running**

   * Run commands directly on the remote server: `$ ssh cs15lfa22@ieng6.ucsd.edu "ls"`
  
      ![Screen Shot 2022-09-29 at 8 48 15 PM](https://user-images.githubusercontent.com/114208205/193186171-6c62e10c-ac83-4538-859e-b6f8ea429e29.png)

   * Run *multiple commands* on the same line by **using semicolons**: `$ cp WhereAmI.java; javac WhereAmI.java; java WhereAmI`
  
     <img width="571" alt="Screen Shot 2022-09-29 at 5 45 42 PM" src="https://user-images.githubusercontent.com/114208205/193185880-bfefc8ff-dece-4a36-b9b1-1ad7effd7219.png">
  
   * **Up-arrow** on your keyboard: recall the last command that was run. 


