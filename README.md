# Introduction to Linux course
In this repo I will explain the concepts I learned when going through a Linux introductory course.

# Table of contents
1. command line basics
2. distributions (distros)
3. package management
4. users
5. sudo
etc..


Today we learned 6 different concepts :


* standard output

Standard output is the successful output that a program shows on the screen after a successful execution.

Example : 
```
ls 
pwd
```


Some commands that don't return a standard output like mkdir can be used with certain options to force it to return a standard output, ex.
```
mkdir -v algo
```


* Redirecting standard output
There are some commands like echo who's sole purpose is to return a standard output to the screen

A very commonly used scenario for echo command is to pair it with a redirection symbol to redirect the output into files (write stuff to files)


```
echo "this will get redirected to a file" > file.txt
```

another common way of redirection is to use double redirect symbol to append or stack more content at the end of the line of the file being created

```
echo "line 2" >> file.txt
```

* Variable declaration and expansion
When writing a shell script we can declare variables that will be used through out of the script execution. For instance

```
NAME="Angelica"
```

We can expand the content of the variable using the dollar sign in bash

```
echo $NAME
```

This knowledge can be stacked by redirecting variables to files with echo the same way we did it on the last lesson

```
echo $NAME > file.txt
```


* For loops
There are many different syntaxes on which someone can declare and use a for loop when scripting in shell/bash. Personally I don't know what the best practices are, but generally the block starts with for ; do and ends with done. One way to solve a problem where you want to execute the same command for a finite number of times could be 

```
for i in $(seq 1 in 100); do
	echo "$i"
done
```

For loops can also be used by iterating "lists" or strings of characters with a defined construction pattern, for example if there's consistently one space between each word, the for loop will take each word as an element of the iteration, example :

```
for var in UNO DOS TRES; do
	echo $var
done
```

Furthermore, the same concept can be applied by expanding variables : 

```
COUNTRIES="USA UK India"

for country in ${COUNTRIES}; do
        echo $country
done
```


* IF statements
If statements can be used in shell scripting not only to compare if a variable is equals to something we want, but also there are several options that simplify the decision making of running a script based on whether a file exists or not, for example the -f in an if statement will return true if the file exists

```
if [[ -f somefile.txt ]]; then
    echo "somefile.txt exists"
fi
```


There are ways to use if statements for multiple decision making, as in every programming language, the 3 main ways on which if statements are constructed are

* simple if statements (like the one above)
* if statements with an else case (or multiple)

```
if [[ -f somefile.txt ]]; then
	echo "somefile.txt exists"
else 
	touch somefile.txt
fi
```


* if elif statements

```
if [[ -f somefile.txt ]]; then
	echo "somefile.txt exists"
elif [[ -f file.txt ]]; then
	echo "file.txt exists"
fi
```



* command line arguments when running a script 
When you run a script, there's a way on which the script can receive "arguments" that can be used during it's execution.

This is actually, as weird as it sounds, one of the most common scenarios on how scripts are constructed in the real world, for instance, if we are running a script that runs on our local computer, we might want to pass something like

```
./script.sh local
```

Inside the script, there's going to be a variable that automatically gets assigned with the 1 in it. To expand it, as with every other variable, we have to use the $ symbol. Following this same example, our script.sh inside could do something like this, 

```
echo $1
```

and the output would be "local"

If you run a script with multiple arguments, for example

```
./script.sh arg1 arg2 arg3 arg4
```

An argument would be assigned to an automatic variable assignation by bash, on where

$1 would equal arg1
$2 would equal arg2
$3 would equal arg3
$4 would equal arg4 


It is however, determined by the order on which you pass the arguments, so for instance

```
./script.sh arg100 arg5
```

echo $1 would equal arg100
echo $2 would equal arg5

usage of this in the real world usually comes paired up with an if statement, for example, we would run a series of steps on a script if we're telling the script through an argument that we're running it on our loca, but do differently if it's being run in production, for example. 

```
./script.sh local
```

```
if [[ $1 == "local" ]]; then
        //series of steps
elif [[ $1 == "prod" ]]; then
        //series of different steps
fi
```
