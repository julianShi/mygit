# mygit
My git command that implements the Myer algorithm. 

**Limitations**
- The tool only supports version control of individual files
- The tool only supports linear version control. That is to say, if you fork from a previous version of the file, the recent versions will lose. 

# Setup
Add the current path to the environment variable
```sh
. ./setupenv.sh
```

# Command options
Display the difference of the file to the current record
```sh
mygit diff <file>
```

Add the changes of the file to the records
```sh
mygit add <file>
```

Display all versions of the file
```sh
mygit log <file>
```

Roll to the previous version of the file
```sh
mygit rollback <file>
```

Roll to the next version of the file
```sh
mygit rollnext <file>
```

Move to certain version of a file. Default is the current version
```sh
mygit checkout <file>
```

# Example
I add the `fib.py` to my directory
```
% mygit add fib.py 
```

The every new file, the `mygit` creates the version control files in `.mygit` directory
```
% ls .pygit 
fib.py
```

The `mygit log` command shows the changes to the files, and the current version of the files. 
```
% mygit log fib.py    

Version #: 1
+ def fib(n):
+   if(n<2):
+     return 1
+   return fib(n-1)+fib(n-2)

Current version: 1
```

Make change to the `fib.py`. The `mygit diff` shows the changes made to this file. The `+` denotes the lines added, the `-` denotes the lines removed. 
```
% mygit diff fib.py              
+ def fib(n,cache):
+   if(n in cache):
+     return cache[n]
- def fib(n):
+   cache[n]= fib(n-1,cache)+fib(n-2,cache)
+   return cache[n]
-   return fib(n-1)+fib(n-2)
```

After adding the file using `mygit add`, you can read the updates using `mygit log` command
```
% mygit add fib.py 
% mygit log fib.py    

Version #: 1
+ def fib(n):
+   if(n<2):
+     return 1
+   return fib(n-1)+fib(n-2)

Version #: 2
+ def fib(n,cache):
+   if(n in cache):
+     return cache[n]
- def fib(n):
+   cache[n]= fib(n-1,cache)+fib(n-2,cache)
+   return cache[n]
-   return fib(n-1)+fib(n-2)

Current version: 2
```
