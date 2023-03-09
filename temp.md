# Finishing the grading script
* to finish up my grading script, I decided to add a .txt file which would receive the output from the junit tests when I ran the grading script so the user can see what their results are without getting lost in the terminal
* I finished writing my grading script by referring to Joe's notes and bash documentation
* here is the finished grading script:
```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf temp
git clone $1 student-submission
echo 'Finished cloning'
if [[ -f student-submission/ListExamples.java ]]
    then echo "ListExamples found"
else 
    echo "Error: ListExamples not found"
fi
mkdir temp
cp student-submission/ListExamples.java temp
cp TestListExamples.java temp
cp -r lib temp
cd temp
javac -cp $CPATH *.java 2> error.txt
if [[ $? -ne 0 ]]
    then echo "Error: Files not compiling"
    exit 1
fi
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > error.txt
if grep -q "FAILURES!!!" error.txt
    then echo "Failed, check error.txt for more details"
else 
    echo "Passed"
fi
```
* now we will test the grading script on several repositories:
1) https://github.com/ucsd-cse15l-f22/list-methods-lab3
* has the same code as the starter from lab 3
* what I expect: the tests will not all pass
* output:
<img width="380" alt="image" src="https://user-images.githubusercontent.com/122491210/223900526-fdf1da83-a499-406a-9eb2-5f1264f1067e.png">
<img width="548" alt="image" src="https://user-images.githubusercontent.com/122491210/223900564-c5522e72-7ea8-4837-8614-1c0526bb2798.png">

2) https://github.com/ucsd-cse15l-f22/list-methods-corrected
* has the same code as the starter from lab 3 corrected
* what I expect: the tests will all pass
* output:
<img width="412" alt="image" src="https://user-images.githubusercontent.com/122491210/223900796-1c04c776-b11d-496e-9d45-6e582f80a1cc.png">
<img width="181" alt="image" src="https://user-images.githubusercontent.com/122491210/223900827-18c75984-e8cd-4539-8cdb-ea07060c408a.png">

3) https://github.com/ucsd-cse15l-f22/list-methods-compile-error
* has a syntax error of a missing semicolon
* what I expect: the tests will not pass
* output:
<img width="448" alt="image" src="https://user-images.githubusercontent.com/122491210/223901099-ab46f281-414b-43a4-99cd-fac91ddd14b5.png">
<img width="301" alt="image" src="https://user-images.githubusercontent.com/122491210/223901143-d8a1deab-4af3-4898-86c0-bb643cadf05a.png">

4) https://github.com/ucsd-cse15l-f22/list-methods-signature
* has the types for the arguments of filter corrected
* what I expect: the tests will all pass
* output:
<img width="412" alt="image" src="https://user-images.githubusercontent.com/122491210/223901302-fd756602-7af0-4de2-aedb-83df1d01aa08.png">
<img width="177" alt="image" src="https://user-images.githubusercontent.com/122491210/223901335-8e500a51-929d-47f8-a348-5360e5c25aec.png">

5) https://github.com/ucsd-cse15l-f22/list-methods-filename
*  has a great implementation saved in a file with the wrong name
* what I expect: the tests will not pass
* output:
<img width="457" alt="image" src="https://user-images.githubusercontent.com/122491210/223901452-880ed081-ea13-4d7c-842f-077d9ccb95e0.png">
<img width="388" alt="image" src="https://user-images.githubusercontent.com/122491210/223901501-0c7f4de1-32ce-4724-9d97-9eaa0a1d4006.png">

6) https://github.com/ucsd-cse15l-f22/list-methods-nested
* has a great implementation saved in a nested directory
* what I expect: the tests will not pass
* output:
<img width="461" alt="image" src="https://user-images.githubusercontent.com/122491210/223901636-b7e3ddf9-ef8c-4e03-81e5-93aeeff72c89.png">
<img width="395" alt="image" src="https://user-images.githubusercontent.com/122491210/223901702-bd0558c7-faec-4303-9aa6-a4a65e8f3294.png">

7) https://github.com/ucsd-cse15l-f22/list-examples-subtle
* has more subtle bugs
* what I expect: the tests will not all pass
* output:
<img width="399" alt="image" src="https://user-images.githubusercontent.com/122491210/223901842-3078ab6f-78bc-47ed-95c5-bab4ad73c771.png">
<img width="498" alt="image" src="https://user-images.githubusercontent.com/122491210/223901873-93837364-299b-4426-a38e-e5e5829afa49.png">

