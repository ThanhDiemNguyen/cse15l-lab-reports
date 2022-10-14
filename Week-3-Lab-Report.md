# Week 3 Lab Report - Servers and Bugs
## Part 1: Simplest Search Engine Web server

---
* **SearchEngine.java**

```
import java.io.IOException;
import java.net.URI;
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;
import java.lang.String;

class Handler implements URLHandler {
    List<String> list = new ArrayList<>();
    public String handleRequest(URI url) {
        /* Home path */
        if (url.getPath().equals("/")){
            return "Welcome to my search engine!";
        } 
        /* path for searching */
        else if (url.getPath().equals("/search")) {
            String results = "";
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                results += String.join("  ", SearchEngine(parameters[1], list));         
            }
            return results;
            
        } 
        /* path for adding a new string to the list */
        else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) { 
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    list.add(parameters[1]);       /* add keywords in to the list */
                    return "";
                } 
            }
            return "404 Not Found!";
        }
    }
    /*
     * searching for a String in a list
     */
    private List<String> SearchEngine(String search, List<String> list) {
        List<String> results = new ArrayList<String>();
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).contains(search)) {
                results.add(list.get(i));
            }
        }
        return results;
    }
}

class SearchEngine {
     public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
    
}
```



**1. Home path:** 

   ![image](https://user-images.githubusercontent.com/114208205/195788974-d78036ab-abbf-4ea9-ae78-d0a885e73e90.png)
 * This is the home part if the path is "/". The method `public String handleRequest(URI url)` is called on the first case `if (url.getPath().equals("/"))` - the values of the relevant arguments. If those values change, the program will check other cases of this method and return the corresponding result.
   
**2. Path for Adding**

   ![image](https://user-images.githubusercontent.com/114208205/195801696-002e2ae5-d67c-4514-83b3-9e4cd22eac09.png)
   ![image](https://user-images.githubusercontent.com/114208205/195801776-f8028e30-9ca7-4f01-8e72-b81bc4e27424.png)
 * This is the adding path if the path is "/add". The method `public String handleRequest(URI url)` is called.
 * Detailly focussing this code:
    <img width="568" alt="image" src="https://user-images.githubusercontent.com/114208205/195805172-3df461a2-3766-4b81-97ad-ede7e7ea9aef.png">
 * If the **url** contains "add", the program will add the string after string "=" to the **list** (created in class Handler).
 * For adding, we use add() with String type in argument. 
 * After run two urls above, the **list** will be [pineapple apple]   
 * In this path, we only add string to the list, so the program will return nothing like two screenshots above.
  
**3. Path for Searching**

   ![image](https://user-images.githubusercontent.com/114208205/195802295-182f3cf5-9b22-4acf-a336-a94e6b735a57.png)
   
  * This is the searching path if the path is "/search". The method `public String handleRequest(URI url)` and `private List<String> SearchEngine(String search, List<String> list)` are called.
  * If the **url** contains "search", the program will search the string after string "=" in the list.
  * For searching, we use the method **SearchEngine**. The method **SearchEngine** take two arguments, including a Sring (input need to search) and a List (contains the added string from the adding path).
  * We call *SearchEngine(parameters[1], list)*. In this screenshot,the string "app" (*parameters[1]*) will be searched in the list [pineapple apple] (*list*). Both strings *pineapple* and *apple* contain the string *app*, so the result wwil be `pineapple apple`
  * If we change the values of parameters[1] to a string "pine". Because only string *pineapple* contains *pine*. The result likes below:
  
    ![image](https://user-images.githubusercontent.com/114208205/195812017-8c354f4b-9f6c-48d6-a391-d2dca8e20494.png)
    
  * If we change the values of parameters[1] to a string "Thanh", which is not contained in any string in the list. -> result is a Null String.
   
    ![image](https://user-images.githubusercontent.com/114208205/195812608-394e939f-5650-4fcc-be24-61080ac4fbd4.png)
     
**4.** For other paths, the program wil return "404 Not Found!"

   ![image](https://user-images.githubusercontent.com/114208205/195813318-495fc31f-86be-417d-87d5-9014822be2f8.png)
      
   ![image](https://user-images.githubusercontent.com/114208205/195813411-d637db5d-336b-4f2c-9641-28b179137842.png)


## Part 2: Bugs and teting

---

### 1. List Methods - filter 

   * The failure-inducing input (the code of the test)
    
      ![image](https://user-images.githubusercontent.com/114208205/195928877-09475af0-0e3f-411d-81f9-f84473ff60cd.png)
     
   * The symptom (the failing test output)
       
      ![image](https://user-images.githubusercontent.com/114208205/195929032-f40c0b93-37c0-4e07-aad3-4fdf43a24f50.png)

   * The bug (the code fix needed)
     ![image](https://user-images.githubusercontent.com/114208205/195938709-321cfa36-5558-448e-bac8-cedff57ebe76.png)
     
     Change `result.add(0,s);` to `result.add(s);`
      
   * Connection between the symptom and the bug
     The symptom show the order of the list *result* is reversed. This happens because of the statement `result.add(0,s);`, which adds a new element at index 0. Since the element added later will always come before the old one -> the order of the list is reversed.
     In my test, the input is [apple app pineapple]. The method filter will check the string "app" with each elements in the list. Starting with the index 0, it's true -> add "apple" to the list *result* at the index 0. Then, similarly add "app" to the list *result* at the index 0 -> the index of "apple" is 1. Finally, add "pineapple" to the list *result* at the index 0 -> the index of "app" is 1 and "apple" is 2. The output for this method is [pineapple app apple]. But the expected output is [apple app pineapple]. 
     So, this method need to change to add(string) without index -> the bugs is solved.
### 2. Array Methods
   * The failure-inducing input (the code of the test)
   
   <img width="146" alt="image" src="https://user-images.githubusercontent.com/114208205/195942202-fd643cdd-b072-4eee-855b-8e1e35355e11.png">

   * The symptom (the failing test output)
   
   <img width="146" alt="image" src="https://user-images.githubusercontent.com/114208205/195942474-49cf07e3-7a48-4696-ad52-aff1e9dca673.png">

   * The bug (the code fix needed)
   
   <img width="146" alt="image" src="https://user-images.githubusercontent.com/114208205/195942573-877ea987-f304-471c-8008-363a85bcb5ce.png">
    Change `arr[i] = newArray[arr.length - i - 1];` to `newArray[i] = arr[arr.length - i - 1];` and return *newArray* instead of *arr*
   * Connection between the symptom and the bug
   This symptom is the newArray is {0 0 0 0 0}, but the expected one is {9,7,5,3,1}.
   Check the original code 
   ```
   static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return ;
   }
   ```
   
   My input1(arr) is {1 3 5 7 9} -> arr.length is 5
   i = 0; input1[0] = newArray[4] = 0
   i = 1; input1[1] = newArray[3] = 0 
   i = 2; input1[2] = newArray[2] = 0 
   i = 3; input1[3] = newArray[1] = 0 
   i = 4; input1[4] = newArray[0] = 0 
   return input1 = {0 0 0 0 0}
   
   -> This method need to assign value of *arr* to value of *newArray* and return *newArray* -> the bugs is solves.
   
   Check the new code:
   ```
   static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
   }
   ```
   My input1(arr) is {1 3 5 7 9} -> arr.length is 5
   i = 0 newArray[0] = input[4] = 9
   i = 1 newArray[1] = input[3] = 7
   i = 2 newArray[2] = input[2] = 5
   i = 3 newArray[3] = input[1] = 3
   i = 4 newArray[4] = input[0] = 1
   
   return newArray = {9 7 5 3 1} -> true
   
   


