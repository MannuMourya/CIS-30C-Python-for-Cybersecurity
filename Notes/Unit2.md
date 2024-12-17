- **sys modules** allows us to interact with the interpreter and contains information related to execution progress, updates by the interpreter and series of functions and low-level objects
- **sys.argv** array that contains arguments in the command line 
	- sys argv [0] = the first index includes the name of the script 
	- Remaining item in argv list include arguments about the next command line
	- If we pass 3 or more argumetns, sys.argv contains 4 objects
example 1 :
```python
import sys 
print("This is the name of the script:", sys.argv[0]) # give you file name
print("This number of arguments is:", len(sys.argv)) # no of argument 
print("The arguments are:",str(sys.argv))  
print("The first arguments is ",sys.argv[1])
print("The second argument is",sys.argv[2])
```
example 2 :
```python
import sys
print("platform:",sys.platfrom) # returns the currrent os 
print(sys.stdout.write("writing in standard output")) 
print("Python Version:",sys.version) # retruns the interpreter version 
print("System encoding.",sys.getfilessystemencoding()) # encoding used by system
print("default encoding:",sys.getdefaultencoding())
print("Path environment variable:",sys.path)
```

- **os module** operating system module is the best mechanism to access different function in the operating system
- Using this module is dependent on OS platform
	- Different commands between Windows, Linux and macOSx bacause of different file system.
Example 3 : Interact with OS, file system and permission to check whether the text file passed as a command-line argument exists as a file in the current path and the current user has read permission to that file 
```python
import sys
import os 

if len(sys.argv) == 2
	filename = sys.argv[1]
	print(filename)

	if os.path.isfile(filename):
		print('[+]'+ filename +' does exit.')
		exit(0)
	if not os.path.isfile(filename):
		print('[+]' + filename + ' does not exist.')
		exit(0)
	if not os.access(filename, os.R_OK):
		print('[+]' + filename + 'access denied.')
		exit(0)
```

- Using os module to list the content of the current working directory with the os.getcws() method 
```python
import os 
pwd = os.getcwd()
list_directory = os.listdir(pwd) # just exeute the listing command of os 
for directory in list_directory
	print('[+]',directory)
```
- os.system(): execute shell command 
- os.listdir(path): returns a list with the contents of the directory passed as an argument
- os.walk(path): navigates all the directory in the provided path directory and returns path directory, names of the subdirectories and a list of filenames in the current path 
```python
import os
for root,directories,files in os.walk(".",topdown=False)
# iterate over the current root 
	for file_entry in files:
		print('[+]',os.path.join(root,file_entry))
	for name in directories:
		print('[++]',name)
```
- os walk can act as a generator function and returns a generator object that implements iteration protocols 
	- returns a tuple that contains current path as a directory name 
	- list of subdirectory name
	- list of non-directory filename

Example 6 : Count the number of files in the current directory using os.path.splitext(filename) to return the file name and extension 
```python
from collection import Counter
counts = Counter()
for currentdir, dirnames, filename in os.walk('.'):
	for filename in filenames:
		first_part, extension = os.path.splitext(filename)
		counts[extension]+=1
	for extension,count in counts.items():
		print(f"{extension:8}{count}")
```

**Platform module** this module in python helps you determine the operating system of the system 
- platform.system() : returns the type of operating system
Example 7 : Display command depending the returned OS type
```python
import platform 
operating_system == platform.system()
print("Your operating system is",operating_system)

if(operating_system == "Windows"):
	ping_command = "ping -n 2 127.0.0.1"
elif(operating_system == "Linux"):
	ping_command = "ping -c 2 127.0.0.1"
else:
	ping_command = "ping -c 3 127.0.0.1"

print(ping_command)
```

**subprocess module** : invoke and communicate with python processes, send data input, and receive output information. 
- Best used in Linux or with C- compiler
- Use to execute and communicate with OS commands or start programs 
- use call() to invoke a process 
- use popen() to start new process that runs specific command
- use terminate() to kill the process running the command
Example 8 : ping google.com using Popen()
```python
import subprocess 
import sys
command_ping = '/bin/ping'
ping_parameter = '-c 1'
domain = "www.goolge.com"
p = subprocess.Popen([command_ping,ping_parameter,domain], shell=False, stderr=subprocess.PIPE)
out = p.stderr.read=(1)
sys.stdout.write(str(out.decode('utf-8)))
sys.stdout.flush()
```

 **Working with files and directories** 
 - file.write(string): write string to file
 - file.read(bufsize): reads up to bufsize, number of bytes from the file. size is optional. it will read the entire file
 - file.readline([bufsize]): reads one line form the file
 - file.close(): close file and destroys the file object 
Example 10 : open, write string to file, test.txt, and close file
```python 
def main():
	with open('test.txt', 'w')as file:
		file.write("this is a test file")
if  __name__ == '__main__':
	main()
```
- `with` is a context manager that automatically handles opening and closing the file. When the `with` block is finished, the file is closed automatically, even if an error occurs within the block. This is a cleaner and safer way to handle files.


**shutil module** : this module is used for high-level operation, such as copy, remove, archieve files
Example : use zipfile module to read file in zip folder .. use yield() to return file name in the zip folder 
```python
import zipfile
def list_files_in_zip(filename):
	with zipfile.ZipFile(filename) as myzip:
		for zipinfo in myzip.infolist():
			yield zipinfo.filename

for filename in list_files_in_zip("files.zip"):
	print(filename)

```

**Threads** are streams that can be scheduled by the OS and executed across a single core processor concurrently or in parallel across multiple cores in the processsor
**threadin** module: constructs higher-level threading interfaces on top of the lower level \_thread module
	- threading module contains Thread() class that we need to extend to create out own execution threads \
		- thread class constructor accepts 5 types of argumetns:
			- groups 
			- target
			- name
			- args
			- kwargs
		- run() is used to execute the threads 
		- thread.join() is used to wait for the thread to finish. it blocks the thread until the thread finish its execution 
- 2 type of threads : 
	- kernel-level threads : low-level threads. users do not interactive with this type of threads 
	- user level threads high level threads. users can interact with this type threads 
	- In Python shell , use help(thread.Thread) command
Example 12 : create 4 threads using threading module 
```python
import threading
import time

num_threads = 4 

def thread_message(message):
	global num_threads
	num_threads -= 1
	print('Message from thread %s\n' %message)
while num_threads > 0 :
	print(" I am the %s thread" %num_threads)
	threading.Thread(target=thread_message("I am the %s thread"%num_threads)).start()
	time.sleep(0.1)
```


Further Reading :
1. https://docs.python.org/3/library/sys.html
2. https://docs.python.org/3/library/os.html
3. https://docs.python.org/3/library/subprocess.html
4. https://docs.python.org/3/library/threading.html