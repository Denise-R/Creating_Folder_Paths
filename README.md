Denise Rauschendorfer

10/13/2022


# __Creating Folder Paths__

In this repository a function, "<span style="color:red">creating_folder_paths</span>", is defined that creates folder paths on your mac/pc to match the folder paths used in another source code. This function is useful if you are trying to run source code that contains.....

The following code was executed using Python 3.10. 

## __Defining the function__

### __Section 1:__
In order to run the following code, the modules '<span style="color:red">re</span>' and '<span style="color:red">os</span>' need to be imported.

```
import re
import os
```


### __Section 2:__

*Note: All of <span style="color:orange">Sections 2-7</span> are contained within the 'def creating_folder_paths(source_file_name):'*

To accomplish this, the following steps are taken:
1. <span style="color:red">def</span> is used to begin defining the function <span style="color:red">creating_folder_paths</span> with the variable <span style="color:blue">source_file_name</span>.
2. The <span style="color:blue">filename</span> that will be used to convert the source code into a .txt titled "<span style="color:blue">code_search.txt</span>" is created.
3. The <span style="color:blue">source_code</span> is then opened in read (<span style="color:blue">r</span>) mode. 
4. A for loop is created to iterate through each line in the <span style="color:blue">source_code</span>.
5. Within this for loop the <span style="color:blue">code_search.txt</span> (named <span style="color:blue">filename</span>) is opened in append (<span style="color:blue">r</span>) mode. 
6. A second for loop is created that iterates through each character within every line of the <span style="color:blue">source_code</span>.
7. Within this nested for loop, an if/else statement is used to change any "\" character to "/" if nesessary and append the character to the <span style="color:blue">code_search.txt</span> file. 
8. Once this process has repeated for all the the characters in every line of <span style="color:blue">source_code</span>, the for loops are broken and the files are closed.

```
def creating_folder_paths(source_file_name):
    filename = "code_search.txt"
    source_code = open(source_file_name, "r")
    for line in source_code.readlines():
        with open(filename, 'a') as f:
            for i in line:
                if i == "\\":
                    i = "/"
                    f.write(i)
                else:
                    f.write(i)
        f.close()
    source_code.close()
```


### __Section 3:__
open the .txt, read each line and check if "C:..." exists in that line. If it does add it to list.

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">list</span> is created.
2. <span style="color:blue">filename</span>, the shorthand for <span style="color:blue">code_search.txt</span>, is opened in read (<span style="color:blue">r</span>) mode. 
3. A for loop is created to iterate through every line in <span style="color:blue">filename</span>.
4. Within the for loop, a regular expression is used to search for any file path saved to the C drive.
5. Nested within the for loop, an if statement is used to save any string of characters that matches the regular expression to <span style="color:blue">list</span>.
6. Once this process has repeated for every <span style="color:blue">line</span> in <span style="color:blue">f</span>/<span style="color:blue">filename</span>, the for loop is broken and the file is closed.

```
    list = []
    f = open(filename, "r")
    for line in f.readlines():
        x = re.findall("\"C:.+\"", line)
        if x != []:
            list.append(x)
    f.close()
```


### __Section 4:__
Checking to see if you want all the folder paths found in the txt

To accomplish this, the following steps are taken:
1. The <span style="color:blue">question</span>, <span style="color:blue">possible_reply</span>, and <span style="color:blue">syntax_error</span> text strings are created.
2. A list titled <span style="color:blue">list_keep</span> is created.
3. A for loop is created to iterate through each item in <span style="color:blue">list</span>. Remember that <span style="color:blue">list</span> was created in <span style="color:orange">Section 3</span> and contains any string of characters from the txt version of the source code that begins with '"C:' and ends with '"'. 
4. The <span style="color:red">input</span> function is used to ask the user if they want to use <span style="color:red">item</span>, a selected character string, to create a folder path. 
5. Within this for loop an if/elif/else statemant is used. If the user selects "A" or "a" to indicate they want to use <span style="color:red">item</span> to create a folder path, then <span style="color:red">item</span> is added to <span style="color:blue">list_keep</span>. If the user selects "B" or "b" to indicate they do not want to use <span style="color:red">item</span> to create a folder path, then the loop continues to the next <span style="color:red">item</span>. Finally, if the user does not input a valid response ("A", "a", "B", or "b"), a <span style="color:blue">syntax_error</span> is printed in console and the loop continues. 
6. Once this process has repeated for every <span style="color:red">item</span> in <span style="color:blue">list</span>, the for loop is broken.

```
    question = "Do you want to make a set of nested folders based on the string: "
    possible_reply = "?\n A. Yes\n B. No\n"
    syntax_error = "Syntax Error: You did not enter a valid response. Only 'A', 'a', 'B', or 'b' are valid responses."
    list_keep = []
    for item in list:
        answer = input(question + str(item) + possible_reply)
        if answer == "A" or answer == "a":
            list_keep.append(item)
        elif answer == "B" or answer == "b":
            continue
        else:
            print(syntax_error)
```


### __Section 5:__
splitting the file location into the separate folders

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">list1</span> is created.
2. A for loop is created to iterate through each <span style="color:blue">item</span> in the list <span style="color:blue">list_keep</span> that was created in <span style="color:orange">Section 4</span>.
3. Within this for loop, each <span style="color:blue">item</span> is converted into a string titled <span style="color:blue">str_item</span>. A regular expression is then used to search through <span style="color:blue">str_item</span> and find every sring of characters contained between, but not containing, two '/'. This list of  character strings are then saved as <span style="color:blue">x</span>. For example, if <span style="color:blue">str_item</span> = ['"C:/folder1/folder2/folder3/file.txt"'], then <span style="color:blue">x</span> = ['/folder1/folder2/folder3/'].
4. Each <span style="color:blue">x</span> is then converted into a string titled <span style="color:blue">y</span> and <span style="color:blue">y</span> is divided into separate strings whereever there is a '/'. This new list of character strings are then saved as <span style="color:blue">z</span> and appended to span style="color:blue">list1</span>. For example, if <span style="color:blue">y</span> = ['/folder1/folder2/folder3/'], then <span style="color:blue">z</span> = ["['", 'folder', 'folder2', 'folder', "']"].
5. Once this process has repeated for every <span style="color:red">item</span> in <span style="color:blue">list_keep</span>, the for loop is broken.

```
    list1 = []
    for item in list_keep:
        str_item = str(item)
        x = re.findall("/.+/", str_item)
        y = str(x)
        z = re.split("/", y)
        list1.append(z)
```


### __Section 6:__
removing "['" and "]'" 

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">list2</span> is created.
2. A for loop is created to iterate through each <span style="color:blue">i</span> in the list <span style="color:blue">list1</span> that was created in <span style="color:orange">Section 5</span>. *Note: <span style="color:blue">list1</span> contains a list of lists.*
3. Within this for loop,the first and last indecies of <span style="color:blue">i</span> are removed. The first and last indecies are "['" and "]'" and were created when <span style="color:blue">y</span> was converted into a string in <span style="color:orange">Section 5</span>.
4. A new list titled <span style="color:blue">list3</span> and a sceond for loop that iterates through each item, <span style="color:blue">j</span>, in each <span style="color:blue">i</span> list are created.
5. Within this for loop, an if/else statement is used to remove any empty character strings ('') from <span style="color:blue">j</span> and add every other value of <span style="color:blue">j</span> to <span style="color:blue">list2</span>. *Note: any empty character strings ('') is created whenever folder directories are distinguished using "//" or "\\" instead of "/" or "\".*
6. Once this process has repeated for every <span style="color:red">j</span> in <span style="color:blue">i</span> and <span style="color:red">i</span> in <span style="color:blue">list1</span>, the for loops are broken.

```
    list2 = []
    for i in list1:
        i = i[1:-1]
        list3 = []
        for j in i:
            if j == '':
                continue
            else:
                list3.append(j)
        list2.append(list3)
```


### __Section 7:__
finding parent dir for each folder, checking if folder path exists, if i doent exist making the folder

To accomplish this, the following steps are taken:
1. A for loop is created to iterate through each <span style="color:blue">i</span> in the list <span style="color:blue">list_keep</span> that was created in <span style="color:orange">Section 4</span>.
2. Within the for loop, the index of each <span style="color:blue">i</span> in <span style="color:blue">list_keep</span> is saved as <span style="color:blue">x</span>.
3. A second for is created to iterate through each <span style="color:blue">j</span> item in <span style="color:blue">list2</span> that corresponds to the index of <span style="color:blue">list_keep</span>. *Note: if <span style="color:blue">list_keep[0]</span> = ['"C:/folder1/folder2/folder3/file.txt"'], then <span style="color:blue">list2</span>[0] = ['folder1', 'folder2', 'folder3'].*
4. Within this second for loop, <span style="color:blue">i</span> is converted into a string <span style="color:blue">y</span> and the first 3 and last 3 indecies of <span style="color:blue">y</span> are removed. These indicies are '['"' and '"']' and are created when <span style="color:blue">i</span> is converted into a string.
5. Next, a regular expression is used to split <span style="color:blue">y</span> into two strings. One containing every character before <span style="color:blue">j</span> and one containing every character after <span style="color:blue">j</span>. This list is saved as <span style="color:blue">z</span>.
6. <span style="color:blue">z[0]</span> is determined to be the parent directory of <span style="color:blue">j</span> and saved as <span style="color:blue">parent_dir</span>.
7. The function <span style="color:red">os.path.join</span> is used to specifiy the folder <span style="color:blue">path</span> that will be created by joining <span style="color:blue">parent_dir</span> and <span style="color:blue">j</span>.
8. Next, the function <span style="color:red">os.path.exists</span> is used to determine if the folder <span style="color:blue">path</span> already exists. This booleen answer is saved as <span style="color:blue">is_exists</span>
9. An if/else statement is used so that if <span style="color:blue">is_exists</span> is 'True', then the user is alerted of this in the console and the loop continues. If <span style="color:blue">is_exists</span> is 'False', then the function <span style="color:red">os.mkdir</span> is used to create the folder <span style="color:blue">path</span> and the user is alerted of this in the console.
10. Once this process has repeated for every <span style="color:red">j</span> in <span style="color:blue">list2[x]</span> and <span style="color:red">i</span> in <span style="color:blue">list_keep</span>, the for loops are broken.

```
    for i in list_keep:
        x = list_keep.index(i)
        for j in list2[x]:
            y = str(i)
            y = y[3:-3]
            z = re.split("" + j + ".+", y)
            parent_dir = z[0]
            path = os.path.join(parent_dir, j)
            is_exist = os.path.exists(path)
            if is_exist == True:
                print("The folder path:" + str(path) + " exists")
                continue
            elif is_exist == False:
                os.mkdir(path)
                print("The folder path:" + str(path) + " was created")
```


## __Using the function__

### __Section 8:__
Now that the function <span style="color:red">creating_folder_paths</span> has been defined, it can be used by specifying the <span style="color:red">source_file_name</span> of the source code. When defining the <span style="color:red">source_file_name</span>, each folder should be deliniated by either "/", "//", or "\\" for <span style="color:red">source_file_name</span> to be a valid entry in python. 

An example of how to use the function <span style="color:red">creating_folder_paths</span> is shown below. 

```
source_file_name = "C:\\folder1\\folder2\\folder3\\folder4\\example.py"
creating_folder_paths(source_file_name)
```


## __Appendix__

### __Compiled Copy of Raw Code:__
```
import re
import os

def creating_folder_paths(source_file_name):
    filename = "code_search.txt"
    source_code = open(source_file_name, "r")
    for line in source_code.readlines():
        with open(filename, 'a') as f:
            for i in line:
                if i == "\\":
                    i = "/"
                    f.write(i)
                else:
                    f.write(i)
        f.close()
    source_code.close()

    list = []
    f = open(filename, "r")
    for line in f.readlines():
        x = re.findall("\"C:.+\"", line)
        if x != []:
            list.append(x)
    f.close()

    question = "Do you want to make a set of nested folders based on the string: "
    possible_reply = "?\n A. Yes\n B. No\n"
    syntax_error = "Syntax Error: You did not enter a valid response. Only 'A', 'a', 'B', or 'b' are valid responses."
    list_keep = []
    for item in list:
        answer = input(question + str(item) + possible_reply)
        if answer == "A" or answer == "a":
            list_keep.append(item)
        elif answer == "B" or answer == "b":
            continue
        else:
            print(syntax_error)

    list1 = []
    for item in list_keep:
        str_item = str(item)
        x = re.findall("/.+/", str_item)
        y = str(x)
        z = re.split("/", y)
        list1.append(z)

    list2 = []
    for i in list1:
        i = i[1:-1]
        list3 = []
        for j in i:
            if j == '':
                continue
            else:
                list3.append(j)
        list2.append(list3)

    for i in list_keep:
        x = list_keep.index(i)
        for j in list2[x]:
            y = str(i)
            y = y[3:-3]
            z = re.split("" + j + ".+", y)
            parent_dir = z[0]
            path = os.path.join(parent_dir, j)
            is_exist = os.path.exists(path)
            if is_exist == True:
                print("The folder path:" + str(path) + " exists")
                continue
            elif is_exist == False:
                os.mkdir(path)
                print("The folder path:" + str(path) + " was created")
```
