# UNIX

## Basic shell commands

UNIX or shell commands have a basic structure:

```bash
command -options target
```

The command comes first (such as cd or ls as we will see later) then any options (always proceeded by a dash (–) and also called flags) and then the target (such as the file to move or the directory to list). These commands are written on the prompt (terminal command line).

__Panic button.__ If you are running a process or program and it is stuck or doing something you don’t want then holding control and pressing c (control+c) will kill the current process and return you to your prompt.

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

Renaming files can be done more tactfully using the rename command. :

```bash
rename my rename my_file.txt
```

The above command replaces 'my' with 'rename' for file `my_file.txt`. This command uses regular expressions (regex) to change filenames, which is extremely useful if you have lots of files with the same pattern that need renaming:

```bash
rename D1_ D01_ *.fastq.gz
```

The above command replaces 'D1_' with 'D01_' for any file ending with '.fastq.gz'.

http://evomics.org/learning/unix-tutorial/

__Basename.__

```bash
for file in *.shp; do echo $(basename $file .shp)_poly.shp; done
```

__Print between two delimiters.__ Useful for extracting one to several sequences from a fasta file.

```bash
awk '/>gene1|>gene2|>gene3/{flag=1;print;next}/>/{flag=0}flag' in.fasta > out.fasta
```

