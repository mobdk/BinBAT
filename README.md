# BinBAT
Create payload that is both binary and batch file at the same time (Windows)


This PoC shows how to create a BinBat.bat file, combining the nature of binary and Windows batch script. Binary files, when compiled don't know what code come after EOF, this is offcause logic, but one can use this like:

copy /B file1.exe+file2.exe file3.exe 

we have a new file file3.exe with two binary files. The nature of Windows batch script (.bat) it is running until broken, by code or by failure.

Take this example, we "merge" a binary file with a batch script, like this:

copy /B binaryfile.dll+script.bat payload.bat

let's say binaryfile.dll a reverse shell and payload.bat only contains echo Hello World, we get this: (USE notepad++)



![Step1](https://github.com/mobdk/BinBAT/blob/master/step1.PNG)
