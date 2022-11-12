# Lab Report 4 –  Vim
## Part 1 - Changing the name of the "start" parameter and its uses to "base"

---

`/start<Enter>cebase<Esc>n.n.:w<Enter>`

* `/start<Enter>` 

  ![image](https://user-images.githubusercontent.com/114208205/201450675-06855b33-3b36-44f3-bd8e-dd5f7a7fb222.png)
  
  The cursor jumping to the start of the first word "start"
  
* `ce`

  ![image](https://user-images.githubusercontent.com/114208205/201450698-7daf2343-8627-48b9-b874-559082705a8d.png)

The cursor switching into input mode and deleting the word "start"

* `base<Esc>`

  ![image](https://user-images.githubusercontent.com/114208205/201450764-d2d888a5-c1bd-4576-97db-ca649d586851.png)
  
  Replacing the text and returning to insert mode.
  
* `n`
  
  ![image](https://user-images.githubusercontent.com/114208205/201450791-08586475-b48c-43c0-81ef-f524ef579075.png)
  
   Repeating the last search from the cursor's position down.
  
* `.`
  
  ![image](https://user-images.githubusercontent.com/114208205/201450801-6fd9a0b2-7b2a-4420-93ff-9ef151ce843a.png)
  
  Repeating last command (Replacing the text and returning to insert mode.)
  
Similarly continue:  
* `n`
  
  ![image](https://user-images.githubusercontent.com/114208205/201450851-c44bd75d-9019-4b53-aa7f-f5e2ae302d84.png)
  
* `.`
  
  ![image](https://user-images.githubusercontent.com/114208205/201450854-7a8b2c2c-324b-46b3-8360-fcaba1732ede.png)

  There is no more the word "start" in the getFiles.
  
* `:w<Enter>`
  
  ![image](https://user-images.githubusercontent.com/114208205/201468695-d81f7583-96e1-41dd-ac6b-01a110f57269.png)


  Saving the changes.
  
  Also, by coming up with google, we find use **:%s/<search_term>/<replace_term>/g** to search and replace in Vim, so the way `:%s/start/base/g` is a better way than my way. But it will lead to some problems when replace the "start" (Server.start()) in class DocSearchServer. 
  
   Details:
  
  ![image](https://user-images.githubusercontent.com/114208205/201463458-69d48f65-0ee0-4287-9e8a-75df9c471553.png)
  
  -> need to change the word "Server.base" to "Server.start" in file DocSearchServer.java using `:%s/Server.base/Server.start/g`
  
 ![image](https://user-images.githubusercontent.com/114208205/201468381-7007b6e7-f114-4d86-bdae-db9ec717ffd6.png)
 
![image](https://user-images.githubusercontent.com/114208205/201468416-1bf17bdd-a476-40ed-b5c9-e32676e5d95c.png)




## Part 2

---
### Report how long it took you to make the edit in seconds in both styles, and any difficulties or details that came up in doing so.
  
  The first way - edit on the Visual Studio Code and scp to ieng6 server: it takes 450 seconds.
  The second way: edit on ieng6 via Vim: it take 400 seconds.
  
### Which of these two styles would you prefer using if you had to work on a program that you were running remotely, and why?

  If you had to work on a program you were running remotely, the second way would be more appropriate. Because changing Visual code and scp to ieng6 every time change is very laborious. Especially if the copy file needs large memory, it will take a long to wait on each copy.
  
### What about the project or task might factor into your decision one way or another? (If nothing would affect your decision, say so and why!)

  I think the complexity (in memory) and the way a project compiles (run locally or remotely) is the deciding factor on which method to use. If a task can run locally, we can choose VSCode to edit because of the mouse's familiarity.
  
