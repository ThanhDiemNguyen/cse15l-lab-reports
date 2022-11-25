# Lab Report 5 – Autograding Script

## Code grade.sh 
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
## Screenshots

<img width="727" alt="image" src="https://user-images.githubusercontent.com/114208205/203740850-cd1320b8-745a-4957-93f1-2d9711bcf338.png">
<img width="766" alt="image" src="https://user-images.githubusercontent.com/114208205/203741140-35bdf446-a5f6-4dfa-a071-32ee931f4c95.png">
<img width="790" alt="image" src="https://user-images.githubusercontent.com/114208205/203741675-972bc121-4d03-4c5a-b1cc-5b55081d1921.png">
<img width="815" alt="image" src="https://user-images.githubusercontent.com/114208205/203742017-bf7e1d28-bb64-4c36-8ce8-bf231b2b6fa2.png">
<img width="768" alt="image" src="https://user-images.githubusercontent.com/114208205/203742204-8c65754d-6876-44d5-85c1-cd8d706de0d9.png">
<img width="758" alt="image" src="https://user-images.githubusercontent.com/114208205/203742427-be742189-9383-499f-a105-57f002280679.png">

## Trace 
 I trace with the link [list-methods-lab3](https://github.com/ucsd-cse15l-f22/list-methods-lab3)
 

