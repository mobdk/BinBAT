# BinBAT
Create payload that is both binary and batch file at the same time (Windows)


This PoC shows how to create a BinBat.bat file, combining the nature of binary and Windows batch script. Binary files, when compiled don't know what code come after EOF, this is offcause logic, but one can use this like:

copy /B file1.exe+file2.exe file3.exe 

we have a new file file3.exe with two binary files. The nature of Windows batch script (.bat) it is running until broken, by code or by failure.

Take this example, we "merge" a binary file with a batch script, like this:

copy /B binaryfile.dll+script.bat payload.bat

let's say binaryfile.dll a reverse shell and payload.bat, we get this: (USE notepad++)


![Step1](https://github.com/mobdk/BinBAT/blob/master/step1.PNG)



Remove MZ from beginning of file, it is very important to follow simple rules each line in your batch script must end with CRLF, I use Notepad++ insert something like ABCDEF and the replace with \r\n


![Step1](https://github.com/mobdk/BinBAT/blob/master/step2.PNG)


Why remove MZ? because this is an bypass method, AV/EDR look for header for identifying file type, now we create a temporary
binary file buf.dll only with content MZ

echo|set /p="MZ"^>C:\Windows\Tasks\buf.dll

the next thing we have to do it "merge" our buf.dll with our batch script, the outcome is our final DLL payload, remember that
the nature of binary files, it never look beyond its EOF.

copy /B C:\Windows\Tasks\buf.dll+C:\Windows\Tasks\Venus.bat C:\Windows\Tasks\tasks.dll

I breake the script with EXIT /b, I have copied dummy data after EXIT /b

I recommend you start with payload coded in C#, because it don't break up, remember the Windows batch engine "think" this is 
a script, at least not the beginning af the file :-)







