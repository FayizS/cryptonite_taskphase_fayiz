## Practicing Piping
I had some problems understanding `tee` and some redirection concepts.<br>
![Tee svg](https://github.com/user-attachments/assets/cc26e509-df82-4800-93f0-f4e220b0563e)<br>
This helped me Understand tee<br>

# Duplicating piped data with tee
Here we intercept `/challenge/pwn` using tee and copy its output to op, which we find the secret argument and how to use it
```console
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee op | /challenge/college
Processing...
WARNING: you are overwriting file op with tee's output...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat op
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "gHK66g3l"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret gHK66g3l | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
```
# Writing to multiple programs
I found this tricky at first, but finally understood that we use >() to make a command act as a file(Process Substitution) which will enable us to substitute this in tee.
```console
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
```
# Split-piping stderr and stdout
We use 2> to redirect the stderr and > to redirect stdout and apply Process Substitution.
```console
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) > >(/challenge/planet)
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
```
