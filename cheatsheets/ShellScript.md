# cheatsheet

[Bash Scripting Cheatsheet](https://github.com/Borosan/bash-scripting-cheatsheet/) and [Sed-Awk Cheatsheet](https://github.com/codenameyau/sed-awk-cheatsheet)


## Frequent used


```
#array for loop
array=("a" "b" "c")
for item in "${array[@]}";
do
   echo $i
done
```





### Example

```
#!/bin/bash

NAME="Payam"
echo "Hello $NAME!"

exit 0
```

### Variables:

```
varname=value                # defines a variable
varname=value command        # defines a variable to be in the environment of a particular subprocess
echo $varname                # checks a variable's value
read <varname>               # reads a string from the input and assigns it to a variable 
let <varname> = <equation>   # performs mathematical calculation using operators like +, -, *, /, %
export VARNAME=value         # defines an environment variable (will be available in subprocesses)
```

```
#Special shell variables
echo $$                      # prints process ID of the current shell
echo $!                      # prints process ID of the most recently invoked background job
echo $?                      # displays the exit status of the last command
echo $0                      # display Filename of the shell script
```

### Quoting:

```
\c             #Take character c literally.
`cmd`          #Run cmd and replace it in the line of code with its output.
"whatever"     #Take whatever literally, after first interpreting $, `...`, \
'whatever'     #Take whatever absolutely literally.

#Example:
match=`ls *.bak`        #Puts names of .bak files into shell variable match.
echo \*                 #Echos * to screen, not all filename as in:  echo *
echo '$1$2hello'        #Writes literally $1$2hello on screen.
echo "$1$2hello"        #Writes value of parameters 1 and 2 and string hello.
```

### Redirection

```
python hello.py > output.txt   # stdout to (file)
python hello.py >> output.txt  # stdout to (file), append
python hello.py 2> error.log   # stderr to (file)
python hello.py 2>&1           # stderr to stdout
python hello.py 2>/dev/null    # stderr to (null)
python hello.py &>/dev/null    # stdout and stderr to (null)
python hello.py < foo.txt      # feed foo.txt to stdin for python
```

### Brace expansion

```
{A,B}	Same as A B
{A,B}.js	Same as A.js B.js
{1..5}	Same as 1 2 3 4 5
```

## Parameter expansions

### Basics

```
name="John"
echo ${name}
echo ${name/J/j}    #=> "john" (substitution)
echo ${name:0:2}    #=> "Jo" (slicing)
echo ${name::2}     #=> "Jo" (slicing)
echo ${name::-1}    #=> "Joh" (slicing)
echo ${name:(-1)}   #=> "n" (slicing from right)
echo ${name:(-2):1} #=> "h" (slicing from right)
echo ${food:-Cake}  #=> $food or "Cake"

length=2
echo ${name:0:length}  #=> "Jo"
```

```
STR="/path/to/foo.cpp"
echo ${STR%.cpp}    # /path/to/foo
echo ${STR%.cpp}.o  # /path/to/foo.o
echo ${STR%/*}      # /path/to

echo ${STR##*.}     # cpp (extension)
echo ${STR##*/}     # foo.cpp (basepath)

echo ${STR#*/}      # path/to/foo.cpp
echo ${STR##*/}     # foo.cpp

echo ${STR/foo/bar} # /path/to/bar.cpp
STR="Hello world"
echo ${STR:6:5}   # "world"
echo ${STR: -5:5}  # "world"
SRC="/path/to/foo.cpp"
BASE=${SRC##*/}   #=> "foo.cpp" (basepath)
DIR=${SRC%$BASE}  #=> "/path/to/" (dirpath)
```

### Substitution

```
${FOO%suffix}	Remove suffix
${FOO#prefix}	Remove prefix
${FOO%%suffix}	Remove long suffix
${FOO##prefix}	Remove long prefix
${FOO/from/to}	Replace first match
${FOO//from/to}	Replace all
${FOO/%from/to}	Replace suffix
${FOO/#from/to}	Replace prefix
```

### Length

```
${#FOO}	Length of $FOO
```

### Default Values

```
${FOO:-val}	$FOO, or val if unset (or null)
${FOO:=val}	Set $FOO to val if unset (or null)
${FOO:+val}	val if $FOO is set (and not null)
${FOO:?message}	Show error message and exit if $FOO is unset (or null)

#Omitting the : removes the (non)nullity checks, 
#e.g. ${FOO-val} expands to val if unset otherwise $FOO.
```

### Comment

```
# Single line comment
: '
This is a
multi line
comment
'
```

### Substrings

```
${FOO:0:3}	Substring (position, length)
${FOO:(-3):3}	Substring from the right
```

### Manipulations

```
STR="HELLO WORLD!"
echo ${STR,}   #=> "hELLO WORLD!" (lowercase 1st letter)
echo ${STR,,}  #=> "hello world!" (all lowercase)

STR="hello world!"
echo ${STR^}   #=> "Hello world!" (uppercase 1st letter)
echo ${STR^^}  #=> "HELLO WORLD!" (all uppercase)
```

## Conditionals:

### Test Operators 

In Bash, the `test` command takes one of the following syntax forms:

* **test EXPRESSION**
* **\[ EXPRESSION ]**
* **\[\[ EXPRESSION ]]**

To make the script portable, prefer using the old test `[` command which is available on all POSIX shells. The new upgraded version of the `test` command `[[` (double brackets) is supported on most modern systems using Bash, Zsh, and Ksh as a default shell.  To negate the test expression, use the logical `NOT` (`!`) operator.

### Checking Numbers

_Note that a shell variable could contain a string that represents a number. If you want to check the numerical value use one of the following:_

```
[[ NUM -eq NUM ]]	Equal
[[ NUM -ne NUM ]]	Not equal
[[ NUM -lt NUM ]]	Less than
[[ NUM -le NUM ]]	Less than or equal
[[ NUM -gt NUM ]]	Greater than
[[ NUM -ge NUM ]]	Greater than or equal
```

### Checking Strings

```
[[ -z STRING ]]	Empty string
[[ -n STRING ]]	Not empty string
[[ STRING == STRING ]]	Equal
[[ STRING != STRING ]]	Not Equal

```

### Checking files

```
[[ -e FILE ]]	Exists
[[ -r FILE ]]	Readable
[[ -h FILE ]]	Symlink
[[ -d FILE ]]	Directory
[[ -w FILE ]]	Writable
[[ -s FILE ]]	Size is > 0 bytes
[[ -f FILE ]]	File
[[ -x FILE ]]	Executable
[[ FILE1 -nt FILE2 ]]	1 is more recent than 2
[[ FILE1 -ot FILE2 ]]	2 is more recent than 1
[[ FILE1 -ef FILE2 ]]	Same files
```

### More conditions:

```
[[ -o noclobber ]]	If OPTIONNAME is enabled
[[ ! EXPR ]]	Not
[[ X && Y ]]	And
[[ X || Y ]]	Or
```

### if statement:

```
#if Statement 

echo -n "Enter a number: "
read VAR

if [[ $VAR -gt 10 ]]
then
  echo "The variable is greater than 10."
fi
```

```
#if..else Statement

echo -n "Enter a number: "
read VAR

if [[ $VAR -gt 10 ]]
then
  echo "The variable is greater than 10."
else
  echo "The variable is equal or less than 10."
fi
```

```
#if..elif..else Statement

echo -n "Enter a number: "
read VAR

if [[ $VAR -gt 10 ]]
then
  echo "The variable is greater than 10."
elif [[ $VAR -eq 10 ]]
then
  echo "The variable is equal to 10."
else
  echo "The variable is less than 10."
fi
```

```
# Nested if Statements
echo -n "Enter the first number: "
read VAR1
echo -n "Enter the second number: "
read VAR2
echo -n "Enter the third number: "
read VAR3

if [[ $VAR1 -ge $VAR2 ]]
then
  if [[ $VAR1 -ge $VAR3 ]]
  then
    echo "$VAR1 is the largest number."
  else
    echo "$VAR3 is the largest number."
  fi
else
  if [[ $VAR2 -ge $VAR3 ]]
  then
    echo "$VAR2 is the largest number."
  else
    echo "$VAR3 is the largest number."
  fi
fi
```

## Loops:

### for:

```
#basic for loop
for i in 1 2 3 4 5
do
   echo "Welcome $i times"
done
```

```
#array for loop
array=("a" "b" "c")
for item in "${array[@]}";
do
   echo $i
done
```

```
#Basic for loop
for i in /etc/rc.*; do
  echo $i
done
```

```
#Ranges
for i in {1..5}; do
    echo "Welcome $i"
done
```

```
#C-Like for loop
for ((i = 0 ; i < 100 ; i++)); do
  echo $i
done
```

```
#with step size
for i in {5..50..5}; do
    echo "Welcome $i"
done
```

### while:

```
n=1

while [ $n -le 5 ]
do
	echo "Welcome $n times."
	n=$(( n+1 ))	
done
```

```
#Using ((expression)) Format With The While Loop
n=1
while (( $n <= 5 ))
do
	echo "Welcome $n times."
	n=$(( n+1 ))	
done
```

```
#for ever
while true; do
  ···
done
```

```
# Reading a test file:
###example1/2:
cat /etc/resolv.conf | while read line; do
  echo $line
done

###example2/2:
file=/etc/resolv.conf
while IFS= read -r line
do
	echo $line
done < "$file"

### Reading A Text File With Separate Fields:
file=/etc/resolv.conf
# set field separator to a single white space 
while IFS=' ' read -r f1 f2
do
	echo "field # 1 : $f1 ==> field #2 : $f2"
done < "$file"
```

### Until:

```
#!/bin/bash

counter=0

until [ $counter -gt 5 ]
do
  echo Counter: $counter
  ((counter++))
done
```

### Case:

```
Case/switch
case "$1" in
  start | up)
    vagrant up
    ;;

  *)
    echo "Usage: $0 {start|stop|ssh}"
    ;;
esac
```

### Functions:

```
# Defining functions:
myfunc() {
    echo "hello $1"
}
# Same as above (alternate syntax)
function myfunc() {
    echo "hello $1"
}
myfunc "John"
```

```
#Returning values:
myfunc() {
    local myresult='some value'
    echo $myresult
}
result="$(myfunc)"
```

```
#Raising errors:
myfunc() {
  return 1
}
if myfunc; then
  echo "success"
else
  echo "failure"
fi
```

```
#Arguments:
$#	Number of arguments
$*	All arguments
$@	All arguments, starting from first
$1	First argument
$_	Last argument of the previous command
```

### Arrays

```
Defining arrays
Fruits=('Apple' 'Banana' 'Orange')
Fruits[0]="Apple"
Fruits[1]="Banana"
Fruits[2]="Orange"
```

```
Operations
Fruits=("${Fruits[@]}" "Watermelon")    # Push
Fruits+=('Watermelon')                  # Also Push
Fruits=( ${Fruits[@]/Ap*/} )            # Remove by regex match
unset Fruits[2]                         # Remove one item
Fruits=("${Fruits[@]}")                 # Duplicate
Fruits=("${Fruits[@]}" "${Veggies[@]}") # Concatenate
lines=(`cat "logfile"`)                 # Read from file
```

```
Working with arrays
echo ${Fruits[0]}           # Element #0
echo ${Fruits[-1]}          # Last element
echo ${Fruits[@]}           # All elements, space-separated
echo ${#Fruits[@]}          # Number of elements
echo ${#Fruits}             # String length of the 1st element
echo ${#Fruits[3]}          # String length of the Nth element
echo ${Fruits[@]:3:2}       # Range (from position 3, length 2)
echo ${!Fruits[@]}          # Keys of all elements, space-separated
```

```
Iteration
for i in "${arrayName[@]}"; do
  echo $i
done
```

### Dictionaries:

```
Defining
declare -A sounds
sounds[dog]="bark"
sounds[cow]="moo"
sounds[bird]="tweet"
sounds[wolf]="howl"
```

```
Working with dictionaries
echo ${sounds[dog]} # Dog's sound
echo ${sounds[@]}   # All values
echo ${!sounds[@]}  # All keys
echo ${#sounds[@]}  # Number of elements
unset sounds[dog]   # Delete dog
```

```
Iteration
Iterate over values
for val in "${sounds[@]}"; do
  echo $val
done
Iterate over keys
for key in "${!sounds[@]}"; do
  echo $key
done
```

### Debugging

```
bash -n scriptname  # don't run commands; check for syntax errors only
set -o noexec       # alternative (set option in script)

bash -v scriptname  # echo commands before running them
set -o verbose      # alternative (set option in script)

bash -x scriptname  # echo commands after command-line processing
set -o xtrace       # alternative (set option in script)
```

## Miscellaneous:

```
#Numeric calculations
$((a + 200))      # Add 200 to $a
$(($RANDOM%200))  # Random number 0..199
```

```
#Inspecting commands
command -V cd
#=> "cd is a function/alias/whatever"
```

```
#Heredoc:
cat <<END
hello world
END
```

```
#printf:
printf "Hello %s, I'm %s" Sven Olga
#=> "Hello Sven, I'm Olga

printf "1 + 1 = %d" 2
#=> "1 + 1 = 2"

printf "This is how you print a float: %f" 2
#=> "This is how you print a float: 2.000000"
```

```
#Reading input
echo -n "Proceed? [y/n]: "
read ans
echo $ans

#Reading  Just one character:
read -n 1 ans    
```

```
#Getting options
while [[ "$1" =~ ^- && ! "$1" == "--" ]]; do case $1 in
  -V | --version )
    echo $version
    exit
    ;;
  -s | --string )
    shift; string=$1
    ;;
  -f | --flag )
    flag=1
    ;;
esac; shift; done
if [[ "$1" == '--' ]]; then shift; fi
```

```
#Check for command’s result
if ping -c 1 google.com; then
  echo "It appears you have a working internet connection"
fi
```


# sed-awk

## TLDR

```bash
$ tldr sed
  sed
  Run replacements based on regular expressions.

  - Replace the first occurrence of a string in a file, and print the result:
    sed 's/find/replace/' filename

  - Replace only on lines matching the line pattern:
    sed '/line_pattern/s/find/replace/'

  - Replace all occurrences of a string in a file, overwriting the file (i.e. in-place):
    sed -i 's/find/replace/g' filename

  - Replace all occurrences of an extended regular expression in a file:
    sed -r 's/regex/replace/g' filename

  - Apply multiple find-replace expressions to a file:
    sed -e 's/find/replace/' -e 's/find/replace/' filename
```

```bash
$ tldr awk

  awk
  A versatile programming language for working on files.

  - Print the fifth column in a space separated file:
    awk '{print $5}' filename

  - Print the second column of the lines containing "something" in a space separated file:
    awk '/something/ {print $2}' filename

  - Print the third column in a comma separated file:
    awk -F ',' '{print $3}' filename

  - Sum the values in the first column and print the total:
    awk '{s+=$1} END {print s}' filename

  - Sum the values in the first column and pretty-print the values and then the total:
    awk '{s+=$1; print $1} END {print "--------"; print s}' filename
    
  - Print line number 
    awk '{ print NR-1 "," $1}' filenam
   
  - Pass shell variable
    awk -v r=$item '{ print r "," $1}'
    
```

## Useful Commands

```bash
# List out the second column in the table.
cat text/table.txt | sed 1d | awk '{ print $2 }'

# Sum the columns in the table.
cat text/table.txt | sed 1d | awk '{ sum += $2 } END { print sum }'

# Kills all processes by name.
ps aux | grep chrome | awk '{ print $2 }' | kill
pkill chrome

# Deletes trailing whitespace.
sed 's/\s\+$//g' filename

# Deletes all blank lines from file.
sed '/^$/d' filename

# Insert 'use strict' to the top of every js file.
sed "1i 'use strict';" *.js

# Append a new line at the end of every file.
sed '1a \n' *

# Generate random numbers and then sort.
for i in {1..20}; do echo $(($RANDOM * 777 * $i)); done | sort -n

# Commatize numbers.
sed -r ':loop; s/(.*[0-9])([0-9]{3})/\1,\2/; t loop' text/numbers.txt
```

## Tutorial
Follow the tutorials here:
- http://www.thegeekstuff.com/tag/sed-tips-and-tricks/
- http://www.grymoire.com/Unix/Sed.html
- http://www.grymoire.com/Unix/Awk.html

```bash
# Unzip data.
unzip data.zip

# Zip data.
zip -r data.zip data/

# Preview the files.
head data/names.csv && tail data/names.csv

# Preview csv columns.
sed -n 1p data/colleges.csv | tr ',' '\n'

# Count the number of lines.
wc -l data/*
```

### Sed Print

```sh
# Print contents of a file.
sed -n '/fox/p' text/*
sed -n '/Sysadmin/p' text/geek.txt

# Print lines starting with `3` and skipping by `2`.
sed -n '3~2p' text/geek.txt

# Print the last line.
sed -n '$p' text/geek.txt

# Prints the lines matching the between the two patterns.
sed -n '/Hardware/,/Website/p' text/geek.txt
```

### Sed Print Line Number

```sh
# Prints the line number for all lines in the file.
sed -n '=' filename

# Prints the line number that matches the pattern.
sed -n '/Linux/=' filename

# Prints the line number in range of two patterns (inclusive).
sed -n '/Linux/,/Hardware/=' filename

# Prints the total number of lines.
sed -n '$=' filename
```

### Sed Delete
The `d` command performs a deletion.

```sh
# Deletes the 3rd line from beginning of file.
sed '3d' text/geek.txt

# Delete every lines starting from 3 and skipping by 2.
sed '3~2d' text/geek.txt

# Delete lines from 3 to 5.
sed '3,5d' text/geek.txt

# Delete the last line.
sed '$d' text/geek.txt

# Delete lines matching the pattern.
sed '/Sysadmin/d' text/geek.txt
```

### Sed Substitute
The `s` command performs a substitution.

```sh
# Simple substituion for the first result.
sed 's/Linux/Unix/' text/geek.txt

# Simple substituion for global instances.
sed 's/Linux/Unix/g' text/geek.txt

# Replace nth instance.
sed 's/Linux/Unix/2' text/geek.txt

# Write matched lines to output.
sed -n 's/Linux/Unix/gp' text/geek.txt > text/geek-sub.txt

# Use regex group for capturing additional patterns (up to 9).
sed 's/\(Linux\).\+/\1/g' text/geek.txt
sed -r 's/(Linux).+/\1/g' text/geek.txt

# Remove the last word.
sed -r 's/\d$//g' text/geek.txt

# Remove all letters.
sed -r 's/[a-zA-Z]//g' text/geek.txt

# Remove html tags (WIP).
sed -r 's|(</?[a-z]+>)||g' text/html.txt

# Commatize any number.
sed ':a;s/\B[0-9]\{3\}\>/,&/;ta' text/numbers.txt
sed -r ':loop; s/\B[0-9]{3}\>/,&/; t loop' text/numbers.txt
```

### Sed Transform
The `y` command performs a transformation.

```sh
# Converts all lowercase chars to uppercase.
sed 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/' text/geek.txt

# Converts all uppercase chars to lowercase.
sed 'y/ABCDEFGHIJKLMNOPQRSTUVWXYZ/abcdefghijklmnopqrstuvwxyz/' text/geek.txt

# Perform a two character shift.
sed 'y/abcdefghijklmnopqrstuvwxyz/cdefghijklmnopqrstuvwxyzab/' text/geek.txt
```

### Sed Multiple Commands
The `-e` flag allows for multiple commands.

```sh
sed -r -e 's/etc\.*//g' -e 's/(\s+)(\))/\2/g' text/geek.txt
```
