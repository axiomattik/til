# Brace Expansion

Bash has a useful feature called 'brace expansion' which allows the generation of arbitrary strings. 

Its forms is:

> *preamble* + { + comma-separated strings | sequence + } + *postscript*

Both the preamble and the postscript are optional.

The preamble is prefixed to each string or term contained inside the curly braces. The postscript is then affixed, going left to right, to each resulting string.

For example: 

```
$ echo a{x,y,z}b
axb ayb azb

$ echo a{1..3}b
a1b a2b a3b

$ echo a{1..10..2}b
a1b a3b a5b a7b a9b
```

Okay, great. But none of those examples are particularly practical. How can brace expansion be useful?

- renaming a file:

`mv file.{txt,md}`

- making backups files:

`cp /path/to/file.txt{,.bak}`

- creating a set of directories:

`mkdir /assets/{img,css,js}`

- or a set of files:

`touch file{1..3}.txt`

- installing multiple libraries

`apt install lib{foo,bar,baz,bizzle}-dev`

- downloading a set of webpages:

`wget https://website.com/comic/page{1..42}.html`

