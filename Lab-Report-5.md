# Lab Report 5 – Autograding Script

## 1. Code grade.sh 
```
# Create your grading script here
#set -e

# Variables 
CPath=lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar 
ERROR=0
GRADE=2

rm -rf student-submission
git clone $1 student-submission

# Check that the student code has the correct file submitted
if [ -e student-submission/ListExamples.java ]
then
    echo "Correct file submitted."
else 
    echo "Incorrect/No ListExamples.java file submitted."
    exit 1
fi

# Get the student code and your test .java file into the same directory

cp student-submission/ListExamples.java ./

# Compile your tests and the student’s code

javac -cp .:$CPath *.java
if [ $? -ne 0 ]
then 
    echo "Compile error!"
    exit 1
fi

# Run the test and grade 
java -cp .:$CPath org.junit.runner.JUnitCore TestListExamples > out.txt

if [ $? -eq 0 ]
then 
    echo -e "Passed all tests.\nGrade: $GRADE/2"
    exit 0
fi

if [ $(grep -c "filter" out.txt) -ne 0 ]
then
    let ERROR+=1
    echo "Failed test filter."
fi
if [ $(grep -c "merge" out.txt) -ne 0 ]
then
    let ERROR+=1
    echo "Failed test merge."
fi

let GRADE-=ERROR
echo "Grade: $GRADE/2"
```
## 2. Screenshots

[list-methods-lab3](https://github.com/ucsd-cse15l-f22/list-methods-lab3)

<img width="727" alt="image" src="https://user-images.githubusercontent.com/114208205/203740850-cd1320b8-745a-4957-93f1-2d9711bcf338.png">

[list-methods-corrected](https://github.com/ucsd-cse15l-f22/list-methods-corrected)

<img width="766" alt="image" src="https://user-images.githubusercontent.com/114208205/203741140-35bdf446-a5f6-4dfa-a071-32ee931f4c95.png">

[list-methods-compile-error](https://github.com/ucsd-cse15l-f22/list-methods-compile-error)

<img width="790" alt="image" src="https://user-images.githubusercontent.com/114208205/203741675-972bc121-4d03-4c5a-b1cc-b55081d1921.png">

<img width="815" alt="image" src="https://user-images.githubusercontent.com/114208205/203742017-bf7e1d28-bb64-4c36-8ce8-bf231b2b6fa2.png">
<img width="768" alt="image" src="https://user-images.githubusercontent.com/114208205/203742204-8c65754d-6876-44d5-85c1-cd8d706de0d9.png">
<img width="758" alt="image" src="https://user-images.githubusercontent.com/114208205/203742427-be742189-9383-499f-a105-57f002280679.png">

## 3. Trace 
 I trace with the link [list-methods-lab3](https://github.com/ucsd-cse15l-f22/list-methods-lab3)
 
 * **Line 9**: `rm -rf student-submission`
  
    Tracing by:
    ```
    rm -rf student-submission >line9.out 2>line9.err
    echo $? >line9.exit
    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203912368-5c689f55-3080-471a-b58c-31cef1bbfa5c.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203912327-efa6ce9e-7f4e-4150-802b-c11fd94ee0ef.png)
    
    Return code: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203912452-582f3d79-7ba8-427f-b38c-19ef1528e6f7.png)
 
 * **Line 10**: `git clone $1 student-submission`
    
    Tracing by:
    ```
    git clone $1 student-submission >line10.out 2>line10.err
    echo $? >line10.exit
    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203913587-4227fb80-e342-40fa-99ed-1f5a264ddf46.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203913543-ec2c8d21-5bf5-404a-a8f9-0e91201526bc.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203913486-4719d9c5-6742-4184-9ec0-702ba67477ba.png)

 * **Line 13-19**: If-statement
    ```
    if [ -e student-submission/ListExamples.java ] 
    then
        echo "Correct file submitted."
    else 
        echo "Incorrect/No ListExamples.java file submitted."
        exit 1
    fi
    ```
    The condition is true because it prints "Correct file submitted." as screenshot in part 2 shown. Therefore, line 16-18 does not run. 
    
 * **Line 22**: `cp student-submission/ListExamples.java`
 
    Tracing by:
    ```
    cp student-submission/ListExamples.java ./ >line22.out 2>line22.err
    echo $? >line22.exit
    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203914778-22e98c32-564e-4773-94f0-d1307e238af3.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203914749-e9ea59b6-6c8a-4978-baad-b5515b896308.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203914717-15b8d8dd-57da-43ab-adaf-55b95ff21bcd.png)

 * **Line 26**: `javac -cp .:$CPath *.java`
 
    Tracing by:
    ```
    javac -cp .:$CPath *.java >line26.out 2>line26.err
    echo $? >line26.exit
    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203915038-3d50d61c-56a1-4fcf-89ff-f4552fe8e621.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203914982-f70d53fe-4de9-4ed3-bd93-2f5f70ef0cc7.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203915007-0b943dc9-9df6-4568-a7bc-f8dd161d5dc3.png)

 * **Line 27-31**: If-statement
    ```
    if [ $? -ne 0 ]
    then 
        echo "Compile error!"
        exit 1
    fi
    ```
    The condition is false because it does not print "Compile error!" as screenshot in part 2 shown. Therefore, line 28-30 does not run. 
    
 * **Line 34**: `java -cp .:$CPath org.junit.runner.JUnitCore TestListExamples`
  
    Tracing by:
    ```
    java -cp .:$CPath org.junit.runner.JUnitCore TestListExamples >line34.out 2>line34.err
    echo $? >line34.exit

    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203915711-374035db-658c-4686-a14a-5e481d11a243.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203915602-47a4ad3a-cda0-47dd-8f3c-a91fd084af67.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203915632-aaa2ee20-b7cc-46be-827e-67975e746d79.png)

 * **Line 35-39**: If-statement
    ```
    if [ $? -eq 0 ]
    then 
        echo -e "Passed all tests.\nGrade: $GRADE/2"
        exit 0
    fi
    ```
    The condition is false because the return code in line 34 is 1. Therefore, line 36-38 does not run. 
    
 * **Line 41-45**: If-statement
    ```
    if [ $(grep -c "filter" out.txt) -ne 0 ]
    then
        let ERROR+=1
        echo "Failed test filter."
    fi
    ```
    The condition is true because there exists the word "filter" in the out.txt (standard output of line 34). 
    
 * **Line 46-50**: If-statement 
    ```
    if [ $(grep -c "merge" out.txt) -ne 0 ]
    then
        let ERROR+=1
        echo "Failed test merge."
    fi
    ```
    The condition is true because there exists the word "merge" in the out.txt (standard output of line 34).
    
 * **Line 52**: `let GRADE-=ERROR`
 
    Tracing by:
    ```
    let GRADE-=ERROR >line52.out 2>line52.err
    echo $? >line52.exit
    ```
   
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203930728-572d6cda-0bd3-47f3-81c7-22b4bc63fd5a.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203930457-159c944c-1390-4199-b9be-08ff7bb9c33c.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203930507-13cf458e-600a-4a8c-91ae-3334a5bdf017.png)

 * **Line 53**: `echo "Grade: $GRADE/2"`
    
    Tracing by:
    ```
    echo "Grade: $GRADE/2" >line53.out 2>line53.err
    echo $? >line53.exit
    ```
    Standard output: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203931147-72cd5ebd-7d5b-4b64-99a4-96c962f261f8.png)

    Standard error: 
    
    ![image](https://user-images.githubusercontent.com/114208205/203931053-878fcd25-8c5f-4b54-8fb4-e25531c00e61.png)

    Return code:
    
    ![image](https://user-images.githubusercontent.com/114208205/203931096-e5ff8015-ebf4-4b4f-986b-9e76d5b46eb3.png)

 

