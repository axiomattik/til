# Bash's Quick Substitution

In Bash	the caret (`^`) can be used to repeat the last command with a substituted argument.

```
$ echo foo
foo
$ ^foo^bar
echo bar
bar
```

But it will only replace one instance of the substring.

```
$ echo foo foo
foo foo
$ ^foo^bar
echo bar foo
bar foo
```

We could use the caret once again to get the desired result.

```
$ ^foo^bar black sheep
echo bar bar black sheep
bar bar black sheep
```

However, if we want to replace all instances of a substring in the previous command, we'd be better off making use of 'word designators' in combination with a special 'substitution modifier'.

```
$ echo foo foo
foo foo
$ !:gs/foo/bar black sheep
echo bar black sheep bar black sheep
bar black sheep bar black sheep
```

Maybe that wasn't quite what I was aiming for. I'll leave it as an exercise for the reader to improve that last command.
