Denise Rauschendorfer

10/13/2022


# __Creating Folder Paths__

In this repository a function is defined that creates folder paths on your mac/pc to match the folder paths used in another source code.

The following code was executed using Python 3.10. 

## __Defining the function__

### __Section 1:__
```
import re
import os
```


### __Section 2:__
```
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


### __Section 7:__
```
source_file_name = "C:\\folder1\\folder2\\folder3\\folder4\\example.py"
creating_folder_paths(source_file_name)

```
