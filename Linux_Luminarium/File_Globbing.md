## Matching with *
'*' is used as a wildcard helping us call /challenge with only a couple characters.
```console
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{Qg0zKeYnWbQX8qP1vPYIZD5K18I.dFjM4QDLyITMzYzW}
```
- Similarly '?' is used as a wildcard for ONLY one character.
## Matching with []
[] is used to provide a set of the characters.
```console
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{gR08-Z0n6zeExNO1QLQmtQPzfXk.dNjM4QDLyITMzYzW}
```
## Matching paths with []
Here we applied the same concept as the previous challenge but we used it in the path.
```console
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{Au9OxnsZSz8ajO7nfJfTXfZqUwe.dRjM4QDLyITMzYzW}
```
## Mixing Globs
Considering the first character of the given file names, I've created a glob.
```console
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{Qk3ZlTS6vLfRWwQ6lzbneozSXgY.dVjM4QDLyITMzYzW}
```
## Exclusionary Globbing
Another glob which helps exclude
```console
hacker@globbing~exclusionary-globbing:/challenge/files$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{gMnRkwgz2iwvgPfYYhV3H59OBAM.dZjM4QDLyITMzYzW}
```
