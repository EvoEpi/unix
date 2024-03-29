# UNIX

## Basic shell commands

UNIX or shell commands have a basic structure:

```bash
command -options target
```

The command comes first (such as cd or ls as we will see later) then any options (always proceeded by a dash (–) and also called flags) and then the target (such as the file to move or the directory to list). These commands are written on the prompt (terminal command line).

__KILL IT!__ If you are running a process or program and it is stuck or doing something you don’t want then holding control and pressing c (control+c) will kill the current process and return you to your prompt.

__Naming files.__ In the sections below you will see that spaces are used to separate commands from options from targets. Thus, it is good practice not to put spaces into file or directories as this will make it difficult to run commands. It is better to use capitals or underscores to separate words in filenames. You should also not use 'weird' symbols such as '\\', '/', '?', '\*', etc. as these are used by the system to do special commands.

__Navigation.__ In order to navigate around the directory structure you first need to know where you are in that structure currently. This is done using the command 'print working directory':

```bash
pwd
```

You can list the contents of the directory using 'list system':

```bash
ls
```

By combining the flags `-l` (long list) and `-h` (human readable) you can list the contents of the directory and meaningful information:

```bash
ls -lh
```

Getting around the directory hierarchy is done using the cd command change directory:

```bash
cd /PATH/TO/DIRECTORY
```

You can move back in directory hierarchy using `../`:

```bash
cd ../../cornus_florida/genome/
```

If you get lost in the directory structure you can return to your home directory with a tilde:

```bash
cd ~
```

__Creating directories and files.__ Use 'make directory' to (as you guessed it) make a directory:

```bash
mkdir my_directory
```

Creating files can be done in many ways. The most common method is to use a command line text editor:

```bash
vim my_file.txt
```

To add text, first press `i` key. You are now free to start entering text. Once you are done entering text, hit the escape/esc key. To quit and save `vim` type colon (`:`), then `x`, and finally enter/return.

Other popular command line text editors include `emacs` and `nano`.

__Copying and moving files.__ Files can be copied using the copy command:

```bash
cp my_file.txt new_file.txt
```

__CAUTION.__ If a file already exists with that name in the directory you are copying to, it will be overwritten by the new one you are copying in. There is no confirmation warning so be careful when copying or moving files.

Files can be moved to a new location using the move command:

```bash
mv my_file.txt ../../cornus_florida/genome/
```

Copying a directory requires the use of a flag:

```bash
cp -r my_directory/ ../../cornus_florida/genome/
```

Moving a file within the same directory renames the original file:

```bash
mv my_file.txt rename_file.txt
```

Renaming files can be done more tactfully using the rename command:

```bash
rename my rename my_file.txt
```

The above command replaces 'my' with 'rename' for file `my_file.txt`. This command uses regular expressions (regex) to change filenames, which is extremely useful if you have lots of files with the same pattern that need renaming:

```bash
rename D1_ D01_ *.fastq.gz
```

The above command replaces 'D1_' with 'D01_' for any file ending with '.fastq.gz'.

__scp.__ Copying files between a server and your local computer is done through a method called `scp` (secure copy):

```bash
scp username@xfer.gacrc.uga.edu:/PATH/TO/FILE/my_file.txt /Users/HAL/Documents/
```

The above command will copy `my_file.txt` from a server to my `Documents` directory.

To transfer a file to your present working directory (`pwd`) replace the path on your local computer with a period (`.`):

```bash
scp username@xfer.gacrc.uga.edu:/PATH/TO/FILE/my_file.txt .
```

__Viewing file contents.__ There are several commands and ways for viewing files without an editor.

To print the entire contents of a file to screen you can use the command `cat`:

```bash
cat <filename>
```

`cat` is not very useful (or advisable) for large files. For large files it is better to use interactive viewers, like `less`:

```bash
less <filename>
```

With `less` the file is then displayed one screen length at a time. Certain commands are then used to go back and forward through the file:

space bar: display the next page  
b: display the previous page  
enter/return: display the next line  
k: display the previous line  
q: quit the viewer  

If a file contains very long lines, these lines will wrap to fit the screen width. This can result in a confusing display, especially if there are, for example, long sequences in your file. To stop this we can use the `-S` flag with `less`:

```bash
less -S <filename>
```

You can scroll horizontally across lines using the arrow keys.

To view a certain number of lines at the start or end of a file we use `head` and `tail`, respectively. For example, to view the file 50 lines:

```bash
head -n 50 <filename>
```

## Advanced shell commands

__Redirect output to file.__ If a command prints information to the screen (standard out) such as cat, echo, ls, grep etc. this output can instead be redirected to a file.

The `>` symbol is used to overwrite the contents of the file with whatever output you specify to redirect to it.

The `>>` is used to append instead of overwrite.

Thus, to place the sentence "One does not simply walk into Mordor." into a file `quote.txt` we type:

```bash
echo "One does not simply walk into Mordor" > quote.txt
```

(echo is a command that prints whatever is after it to the screen)

If we then want to add the contents of `quote.txt` we type:

```bash
echo "They've taken the hobbits to Idsengard" >> quote.txt
```

__Tab completion.__ The tab button can be used to complete file/directory names and do quick lookup of commands.

__Pipe.__ The output from one unix command can be sent as input to another using a pipe. The symbol for this pipe is the vertical bar `|`. For example, the following commands will first 'cut' the fourth column from a bed file, sort that column, count the number of occurences of unique strings, and then sort (in descending order):

```bash
cut -f4 my.bed | sort -nk1,1 | uniq -c | sort -nk1,1
```

__Loops.__ Have a command that needs to be repeated mutliple times? Write a loop! To successfully execute a loop, two features of the shell need to be understood: (i) variables and (ii) wildcards (we saw one earlier).

A __variable__ is a placeholder for some text such as a directory name, filename, number, sentence etc. A variable is always initialised using the name you designate for the variable (e.g. file, direc, superman, x, etc.) It can be whatever you want once it is a single word without spaces or special characters. The variable is then called using a `$` in front of the name.

```bash
MYVAR="Hello world"
echo $MYVAR
```

The asterisk (`*`) is referred to as a wildcard symbol in unix. This allows for matching of filenames, directories etc. that all have a certain sections of their name in common. For example, if all your files start with 'cornus_florida' (e.g. cornus_florida_species.txt, cornus_florida_locations, cornus_florida) these will all be recognised using `cornus_florida*`. Alternatively if they all end with `.txt` you can loop over them all using the `*.txt`.

A for loop has the syntax:

for <variable> in <list>  
do  
\<task1 to repeat for each item in list\>  
\<task2 to repeat for each item in list\>  
\<task3 to repeat for each item in list\>  
done  

Or in a bash shell:

```bash
for <variable> in <list>; do <task1 to repeat for each item in list>; <task2 to repeat for each item in list>; <task3 to repeat for each item in list>; done
```

We can use a for loop to print the numbers 1 to 10 to screen by typing:

```bash
for num in {1..10}; do echo $num; done
```

Lets use a for loop to create 3 directories which will be named `run1`, `run2` and `run3`:

```bash
for num in {1..3}; do mkdir “run”$num; done
```

Loops are then most useful when running a pipeline on multiple samples:

```bash
#!/bin/bash

QUERY=(Alyrata_384_v2.1.cds_primaryTranscriptOnly.fa BrapaFPsc_277_v1.3.cds_primaryTranscriptOnly.fa Crubella_474_v1.1.cds_primaryTranscriptOnly.fa)
DB="Athaliana_447_Araport11.cds_primaryTranscriptOnly.fa"

for i in "${QUERY[@]}"
  do
    blastn -db $DB -query $i -evalue 1E-06 -max_hsps 1 -max_target_seqs 8 -outfmt 6 >> blastn.out
done
```

__Grep.__ Grep is a tool for searching files for a specific content. It has many applications and some will be explained here. The basic syntax of grep is:

```bash
grep \<search pattern\> \<filename\>
```

Flags can be used to modify these results in many useful ways. For example:

grep -n \<search pattern\> \<filename\> will print the line number of the result beside each matching line  
grep -v \<search pattern\> \<filename\> will find the lines which don’t contain the search pattern  
grep -c \<search pattern\> \<filename\> does not return the lines that match but instead returns a count of the number of lines that contained a hit  
grep -i \<search pattern\> \<filename\> use a case insensitive match (meaning B and b are the same thing)  
grep -A 5 \<search pattern\> \<filename\> will print the 5 lines that come after a line that matches the pattern  
grep -B 5 \<search pattern\> \<filename\> will print the 5 lines that come before a line that matches the pattern  

These can then be combined so that, for example, grep -vc <search pattern> <filename> will return a count of the lines that don’t contain the provided search pattern

__.bash_profile, .bashrc, alias and PATH.__


The behaviour of the terminal shell can be modified by adding commands to one of two hidden files: `.bashrc` and `.bash_profile`, which are found in the home directory. In the Mac OSX terminal these files do the same thing. The `.bashrc` runs each time a terminal window is opened whereas `.bash_profile` only runs the first time a terminal is opened.

The two main things we will use the `.bash_profile` file for is creating aliases and modifying the PATH.

An alias allows you to create shortcut commands that point to longer commands, thus saving on time. For example, if we used `ls -lh` often and wanted a shortcut for this we could create an alias `lsl` that would run this command for us.

On a Mac edit the .bashrc:

```bash
vim ~/.bashrc
```

Within this file we will create a new alias for `ls -lh` by typing `alias lsl='ls -lh'`. Save and close the file. Refresh your `.bashrc` to enact the change(s):

```bash
source ~/.bashrc
```

Now if you type `lsl` the command should run as specified.

Aliases can be used to create command shortcuts for any task. This is useful particularly for repeated tasks such as `ssh` and `scp` to locations with long addresses. For instance, lets say in order to `shh` to the university's cluster I had to type:

```bash
ssh username@sapelo2.gacrc.uga.edu
```

This would become tedious. Instead I can create an alias `sapelo2` to enact this command: `alias sapelo2='ssh username@sapelo2.gacrc.uga.edu'`. Thus, I just type `sapelo2` on the terminal and the `ssh` command is run for me.

The commands that are run within the terminal such as `cd`, `less`, `ls` etc. are executable files that have been created and stored in specific folders in the system. The system then knows where to look for these programs by searching in directories specified in the environment variable PATH. You can view your current PATH by typing:

```bash
echo $PATH
```

This will output something like the following, `/usr/local/bin:/usr/bin:/bin`.

This means that the system can run executable programs that are stored in these three folders (separated by the :) without the user having to specify the absolute path to the folder. A user may wish to modify this path to add other folders where such programs can be stored. This is useful for downloaded programs which you want to be able to run.

For instance, if you download the [BLAST+ package from NCBI](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) and store it in your home directory, each time you wish to run `blastn` in the terminal you would have to type the full program path. It is good practise  to create a `bin` folder in a directory (like `home`) to store all downloaded programs. You then add this folder to the path in the `.bashrc`. Thus, if a folder `/home/username/bin/` exists and `blastn` is inside this we can add the folder to the path by editing the `.bashrc` file:

```bash
vim ~/.bashrc
export PATH=$PATH:/home/username/bin
```
Save the `.bashrc` file and exit. You can reload the `.bashrc` file manually again by typing `source .bashrc`.

Any executable program placed in this folder (e.g. `blastn`, `raxml`, `mafft`, etc.) can be called directly from the command line, similar to `cd` etc.

## Useful recipes

__Basename.__

```bash
for file in *.shp; do echo $(basename $file .shp)_poly.shp; done
```

__Print between two delimiters.__ Useful for extracting one to several sequences from a fasta file.

```bash
awk '/>gene1|>gene2|>gene3/{flag=1;print;next}/>/{flag=0}flag' in.fasta > out.fasta
```

__Search and replace.__

```bash
awk  '{gsub("/","\t",$0); print;}' filename
```

```bash
sed -i 's/search/replace/g' filename
```
