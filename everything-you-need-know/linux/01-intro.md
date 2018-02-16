 The  examples  from this exercise are  from  the instructor account: instructor, so you will not see the exact same output.
## The Single Most Useful Unix Command 

The single most useful command learning linux/unix is the man (output the ‘manual’) command. If you forget how to use a specific command, type ‘man [commnad]’: 
```
instructor@local:~$ man man 
MAN(1)               Manual pager utils              MAN(1) 
NAME 
       man - an interface to the on-line reference manuals 
SYNOPSIS 
       man  [-C file] [-d] [-D] [--warnings[=warnings]] [-R 
       encoding] [-L locale] [-m  system[,...]]  [-M  path] 
       [-S  list]  [-e  extension] [-i|-I] [--regex|--wild
       ‐card] [--names-only] [-a] [-u]  [--no-subpages]  [-P 
       pager]  [-r prompt] [-7] [-E encoding] [--no-hyphen
      ‐ation]   [--no-justification]   [-p   string]   [-t] 
       [-T[device]] [-H[browser]] [-X[dpi]] [-Z] [[section] 
       page ...] ... 
       man -k [apropos options] regexp ... 
       man -K [-w|-W] [-S list] [-i|-I] [--regex] [section] 
       term ... 
       man -f [whatis options] page ... 
       man  -l  [-C file] [-d] [-D] [--warnings[=warnings]] 
       [-R encoding] [-L locale]  [-P  pager]  [-r  prompt] 
       [-7]  [-E  encoding]  [-p  string] [-t] [-T[device]] 
       [-H[browser]] [-X[dpi]] [-Z] file ... 
       man -w|-W [-C file] [-d] [-D] page ... 
       man -c [-C file] [-d] [-D] page ... 
       man [-hV] 
       
       DESCRIPTION 
       man is the system's manual pager. Each page argument 
       given  to  man  is  normally  the name of a program, 
       utility or function.   The  manual  page  associated 
       with  each of these arguments is then found and dis
       -played. A section, if provided, will direct  man  to 
       look  only  in  that  section  of  the  manual.  The 
       default action is to search in all of the  available 
       sections,  following a pre-defined order and to show 
       only the first page found, even if  page  exists  in 
       several sections 
```
   
     ... followed by a complete description of how to use the man command ... 

# Navigating the File System
As with all major operating systems, the Unix file system is a hierarchy of directories and files. For those familiar with Windows or MAC OS X, directories are exactly equivalent to folders. 
If you prefer  a graphical user interface (GUI), click on any of the default desktop icons (‘Home’, ‘File System’) or the folder icon in the bottom panel. T


#Where Am I
To ensure you start the exercise in the correct location, execute the cd command: 
```
instructor@local:~$ cd 
```
The  cd  (‘change  directory’)  command,  with  no  arguments,  will  place  you  in  your  home  directory.  The pwd (‘print working directory’) command will print the path to the current directory: 

```
instructor@local:~$ pwd 
/home/instructor  
```
Of course, you should see your user id, not instrctor.

#What's Here
The ls (‘list’) command will list the files and subdirectories in the current directory (the set of files you see 
may not be the same as shown): 
```
instructor@local:~$ ls 
android-sdk                 Documents         Music     sfuhome 
C:\nppdf32Log\debuglog.txt  Downloads         Pictures  Templates 
Desktop                     examples.desktop  Public    Videos  
```

Unix,  like  Windows  and  OS  X,  has  hidden  files  and  directories, which hold  configuration  and  state  information  used  by  the  operating  system  and  various  programs.  To  see  these,  add  ‘-a’  to  the  
command line: 
```
instructor@local:~$ ls -a 
.             Documents         .local         Templates 
..            Downloads         .mozilla       Videos 
android-sdk   examples.desktop  Music          .viminfo 
.bash_logout  .gconf            Pictures       .Xauthority 
.bashrc       .gnome2           .profile       .Xdefaults 
.cache        .gnome2_private   Public         .xscreensaver 
.config       .gstreamer-0.10   .pulse         .xsession-errors 
.dbus         .gvfs             .pulse-cookie 
Desktop       .ICEauthority     sfuhome 
```
Yes,  there  are  lots  of  them.  For  example,  the  .config directory  is  used  by  the  Xfce  window  manager  to  store  configuration  information.  The  file  .bashrc is  executed  by  the  bash  shell  as  it  
starts  up.

How  can  I  determine the difference between files  and directories?  On  many  systems, ls will  produce a color-coded output, but if not, you can use the ‘-F’ flag: 

```
instructor@local:~$ ls -F 
android-sdk@  Downloads/        Pictures/  Templates/ 
Desktop/      examples.desktop  Public/    Videos/ 
Documents/    Music/            sfuhome/ 
```
Directories  have  a  ‘/’  added  to  the  end.  Executable  files  have  an  ‘*’ on  the  end. Other characters are used to indicate other file types. 
By providing either a file or directory name, ls will restrict to just that file or directory. Suppose you
want some details for sfuhome. I can add the ‘-l’ and ‘-d’ flags to my ls command, with the directory name and get: 
```
instructor@local~$ ls -ld sfuhome 
drwx--s--x 11 skristja users 0 Sep 14 13:03 sfuhome 
```
What  does  this  output  sugguest?  Here’s  a  quick  description  of  the  fields: 
* drwx--s--x are the file permissions. These permissions show sfuhome is a directory (the leading ‘d’); allows for reading (browse), writing (create), and executing (access) the directory 
(the next three characters, ‘rwx’); and others can execute files in the sfuhome directory only  if  they  know  the  file  name  (the  characters  ‘--x’  mean  that  others  can  access  the  files  but  not  browse  them).  The  chmod  (‘change  mode’)  command  is  
used  to  manipulate  file  permissions.     
* instructor is the owner of the file. 
* 0 is the size in bytes.  
* Dec 31 13:03 is the time the directory was last modified. 

Notice  many  Unix  commands  use  single-letter  options  and  can be combined with a single ‘-’. Try ‘ls -alF’. Suppose  you  just  want  to  determine  the  files  with  extension  .txt?  Unix  command  shells  support  
wildcard characters in file and directory names. The character ‘*’ matches any string; ‘?’ matches any single character. 

```
instructor@local:~$ ls *.txt 
C:nppdf32Logdebuglog.txt 
instructor@local:~$ ls -d ?o* 
Documents  Downloads 
```
In the second ls command, I asked for a listing of any name that has ‘o’ as the second character. The directories Documents and Downloads matched.

# How Do I Move Around?
To move to another place in the file system, use the cd (‘change directory’) command:
```
instructor@local:~$ cd sfuhome 
instructor@local:~/sfuhome$ pwd 
/home/instructor/sfuhome 
```

Notice the change in the command prompt: 
```
instructor@local:~$ 
```
changed to 
```
instructor@local~/sfuhome$ 
```
The default command prompt displays several pieces of information: 

Remember,  in  a  Unix  command  shell,  the  character  ‘~’  in  a  file  name  is  the  abbreviation  for  your  
home  directory.

#How Do I Create a Directory?
The mkdir (‘make directory’) command will create a new, empty directory: 
```
instructor@local:~/sfuhome$ mkdir Demo 
instructor@local:~/sfuhome$ ls -F 
bin/      CMPT 150/  desktop.ini*  pub_html/ 
cmpt125/  Demo/      personal/     $RECYCLE.BIN/ 
```

What’s in a brand new directory? 
```
instructor@local:~/sfuhome$ ls -aF Demo 
./  ../ 
```

In unix, every directory will have two entries: 
* A single ‘.’ (period) means ‘the current directory’. 
* Two periods, ‘..’, means ‘the parent directory’. 

These abbreviations can be used on the command line: 
```
instructor@local:~/sfuhome$ cd Demo 
instructor@local:~/sfuhome/Demo$ pwd 
/home/instructor/sfuhome/Demo 
instructor@local:~/sfuhome/Demo$ ls .. 
bin      CMPT 150  desktop.ini  pub_html 
cmpt125  Demo      personal     $RECYCLE.BIN 
instructor@local:~/sfuhome/Demo$ cd .. 
instructor@local:~/sfuhome$ 
```
#How Do I Delete a File?
To  experiment  with  deleting  files  and  directories, create an empty file or two  with the touch command: 

```
instructor@local:~/sfuhome$ cd Demo 
instructor@local:~/sfuhome/Demo$ touch worthless 
instructor@local:~/sfuhome/Demo$ ls -l worthless 
-rw-r--r-- 1 instructor users 0 Dec 31 16:45 worthless 
```
Another way is to redirect some output into a file:
```
instructor@local:~/sfuhome/Demo$  echo 'Hi, Mom!' > himom.txt 
instructor@local:~/sfuhome/Demo$ ls -l himom.txt 
-rwxr--r-- 1 instructor users 31 Dec 17 16:48 himom.txt 
```
The echo command  simply  echoes  its  argument.  The  ‘>’  character  redirects  that  output  into  the  file himom.txt.   Use  single  quotes  around  ‘Hi,  Mom!’  The  exclamation  mark  ‘
!’  has  special  meaning  to  the  shell  (beyond  the  scope  of  this  introductory  exercise).  The  file  himom.txt really isn’t executable. You can remove the execute permission with the command ‘chmod a-x’: 

```
instructor@local:~/sfuhome/Demo$ chmod a-x himom.txt 
instructor@local:~/sfuhome/Demo$ ls -l himom.txt 
-rw-r--r-- 1 instructor users 31 Dec 17 16:48 himom.txt 
```

To delete a file, use the rm (‘remove’) command: 
```
instructor@local:~/sfuhome/Demo$ ls 
himom.txt  worthless 
instructor@local~/sfuhome/Demo$ rm worthless 
rm: remove regular empty file `worthless'? y 
instructor@local:~/sfuhome/Demo$ ls 
himom.txt 
```

Normally,  the  Unix  command  line  just executes,  immediately,  with  no  argument.  The  rm command  above  prompted  for  confirmation  because  the  default  CSIL  configuration  creates  an  
alias: 
```
instructor@local~/sfuhome/Demo$ alias rm 
alias rm='rm -i' 
```
The ‘-i’ (interactive) flag is the reason for the prompt. If you’re tired of having your computer ask ‘Are you sure?’ every time you ask it to do something, simply remove the alias:

```
instructor@local:~/sfuhome/Demo$ unalias rm 
instructor@local:~/sfuhome/Demo$ touch worthless 
instructor@local:~/sfuhome/Demo$ ls 
himom.txt  worthless 
instructor@local~/sfuhome/Demo$ rm worthless 
instructor@local:~/sfuhome/Demo$ ls 
himom.txt
```
If you like the opportunity for a second thought, it’s easy to get it back: 
```
instructor@local:~/sfuhome/Demo$ alias rm='rm -i' 
instructor@local:~/sfuhome/Demo$ alias rm 

alias rm='rm -i' 
```

The  proper  location for an  unalias  command  is  in  your  .bashrc file,  where  it  will  take  effect  automatically. This is also a good place to add aliases 
or modify your default search path. The search path is the set of directories, which Unix searches when determining executable files. 

What about deleting a directory? Let’s move from the Demo directory and delete it: 
```
instructor@local:~/sfuhome/Demo$ cd .. 
instructor@local:~/sfuhome$ rm Demo 
rm: cannot remove `Demo': Is a directory 
```
Hmmm . . . not very successful. Some of you may know that there is another command, 
rmdir, specifically for removing directories: 
```
instructor@local:~/sfuhome$ rmdir Demo 
rmdir: failed to remove `Demo': Directory not empty 
```

We  could  remove  Demo/himom.txt and  then  remove  the  Demo directory,  but  it's not  
necessary: 
```
instructor@local:~/sfuhome$ rm -r Demo 
rm: descend into directory `Demo'? y 
rm: remove regular file `Demo/himom.txt'? y 
rm: remove directory `Demo'? y 
instructor@local:~/sfuhome$ ls 
bin      CMPT 150     personal  $RECYCLE.BIN 
cmpt125  desktop.ini  pub_html 
```

The  ‘-r’  flag  (‘recursive’)  tells  the  rm command    to  remove  the  directory  and  its  contents, recursively.  

The ‘-r’ flag can be used in many commands, with the same meaning: Perform the action for the directory and all its contents, recursively. 

# How Do I Move Things Around?
To  copy  or  move  files  and  directories,  let's recreate  the Demo directory  and  himom.txt.

```
instructor@local:~/sfuhome$ mkdir Demo 
instructor@local:~/sfuhome$ cd Demo 
instructor@local:~/sfuhome/Demo$ echo 'Hi, Mom!' > himom.txt 
instructor@local:~/sfuhome/Demo$ ls 
himom.txt
```
The cp (‘copy’) command will copy a file: 
```
instructor@local:~/sfuhome/Demo$ cp himom.txt another.txt 
instructor@local:~/sfuhome/Demo$ ls 
another.txt  himom.txt 
```
You can copy entire directory trees with a single command using the ‘-r’ flag: 
```
instructor@local:~/sfuhome/Demo$ cd .. 
instructor@local:~/sfuhome$ cp -r Demo Demo2 
instructor@local:~/sfuhome$ ls 
bin      CMPT 150  Demo2        personal  $RECYCLE.BIN 
cmpt125  Demo      desktop.ini  pub_html 
instructor@local:~/sfuhome$ ls Demo 
another.txt  himom.txt 
instructor@local:~/sfuhome$ ls Demo2 
another.txt  himom.txt 
```
The mv command (‘move’) will move a file or directory from one place to another. To rename a file, 
simply move it to the new name: 
```
instructor@local:~/sfuhome$ mv Demo/himom.txt Demo2/byemom.txt 
instructor@local:~/sfuhome$ ls Demo 
another.txt 
instructor@local:~/sfuhome$ ls Demo2 
another.txt  byemom.txt  himom.txt
```

Moving a directory works the same way:
```
instructor@local:~/sfuhome$ mv Demo2 NewDemo 
instructor@local:~/sfuhome$ ls 
bin      CMPT 150  desktop.ini  personal  $RECYCLE.BIN 
cmpt125  Demo      NewDemo      pub_html 
instructor@local:~/sfuhome$ ls NewDemo 
another.txt  byemom.txt  himom.txt 
```
If you move or copy a file with the same name, it will be overwritten without complaint: 

```
instructor@local:~/sfuhome$ ls Demo 
another.txt 
instructor@local:~/sfuhome$ ls NewDemo 
another.txt  byemom.txt  himom.txt 
instructor@local:~/sfuhome$ mv NewDemo/himom.txt Demo/another.txt 
instructor@local:~/sfuhome$ ls Demo NewDemo 
Demo: 
another.txt 
NewDemo: 
another.txt  byemom.txt 
```
Be careful! If you would rather have a safety net, you can use the ‘-i’ option for mv and cp.
```
instructor@local:~/sfuhome$ ls Demo 
another.txt 
instructor@local:~/sfuhome$ ls NewDemo 
another.txt  byemom.txt 
instructor@local:~/sfuhome$ mv -i Demo/another.txt NewDemo 
mv: overwrite `NewDemo/another.txt'? n 
instructor@local:~/sfuhome$ ls Demo 
another.txt 
instructor@local:~/sfuhome$ ls NewDemo 
another.txt  byemom.txt 
```
As you can see, typing ‘n’ (no) to the prompt aborts the move. If you like this style, create aliases.  
Notice  that  the  mv command  specifies  a  specific  file  to  move  (Demo/another.txt)  and  only  a directory  (NewDemo)  for  the  target;  this  says  ‘move  the  file  to  the  target  directory;  but  do  not  
change the file name.’ 

```
instructor@local:~/sfuhome$ cd Demo 
instructor@local:~/sfuhome/Demo$ touch "Name With Spaces" 
instructor@local:~/sfuhome/Demo$ ls 
another.txt  Name With Spaces 
instructor@local:~/sfuhome/Demo$ rm Name With Spaces 
rm: cannot remove `Name': No such file or directory 
rm: cannot remove `With': No such file or directory 
rm: cannot remove `Spaces': No such file or directory 
instructor@local:~/sfuhome/Demo$ rm "Name With Spaces" 
rm: remove regular empty file `Name With Spaces'? y 
instructor@local:~/sfuhome/Demo$ ls 
another.txt 
```
The Unix command shells assume spaces are separate parameters. Here, the shell interprets ‘Name With Spaces’ as three separate file names. 

# How Do I See What Is In a File?
In Unix, the file command will tell you what's in a file: 
```
instructor@local:~/sfuhome/Demo$ cd ~/sfuhome 
instructor@local:~/sfuhome$ ls 
bin      CMPT 150  desktop.ini  personal  $RECYCLE.BIN 
cmpt125  Demo      NewDemo      pub_html 
skristja@asb9838n-a07:~/sfuhome$ file Demo 
Demo: setgid directory 
instructor@local:~/sfuhome$ file desktop.ini  
desktop.ini: Little-endian UTF-16 Unicode text, with CRLF, CR line 
terminators 
instructor@local:~/sfuhome$ file /bin/bash 
/bin/bash: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically 
linked (uses shared libs), for GNU/Linux 2.6.24, 
BuildID[sha1]=0xe643cefb2c672ad94e955067c511537ddbab48da, stripped 
```
It  is  a  good  idea  to  use  common  extensions  for  files  (e.g., .pdf for  a  PDF  file)  but  the  file command does not rely on the file name extensi
on. It looks at the content of the file and makes its best guess, but it can be wrong. 

Text files can be dumped to the terminal with the cat command.  The  best  pager  is  a  command  called  less (a  pun  at  the  expense  of  the  less  capable  
pager program called more). 

```
instructor@local:~/sfuhome$ less Demo/another.txt 
Hi, Mom! 
Demo/himom.txt (END) 
```

Type ‘q’ to exit the pager. For serious file manipulation, you will want to use an editor. The two historical command line ascii text  editors  are  vim and emacs.  You  will  want  to  experiment  with  them.  They  have  radically  different approaches to editing, and the choice between them is entirely a matter of personal taste. 
The learning curve is steep for both of them, but they are very powerful when it comes to creating and editing program text. There are many other editors available — ask friends, do some Internet searching,  find  something  that  works  for  you.  Eclipse  has  a  built-in  editor  with  considerable  
knowledge of Java syntax and formatting. To view PDF and Postscript, use the evince viewer. Adobe acroread is also available for PDF 
files. An easy way to read PDF in Ubuntu is to use the graphical file browser, and simply double 
click on the PDF file you want to open. 
