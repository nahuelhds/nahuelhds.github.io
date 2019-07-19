---
lang: en
title: How to delete local and remote tags massively from a git repo in just one line
excerpt: A one-line command to save you hours of manual work
date: '2019-05-12T20:24:33.560Z'
categories:
  - git
keywords:
  - delete-tag
  - local-tag
  - remote-tag
  - massively
  - repository
  - one-line-command
---

![Resultado de imagen para git](https://cdn-images-1.medium.com/max/800/1*4W4fdnO680ysRhFc9ppc8w.jpeg)

### TL;DR. Give me the magic 🧙‍♂️

> **WARNING!** This is a destructive command. Use at your own risk

**Use case:** you want to delete the major version 0 and its children.

First, a dry run…

```sh
SEMVER=0 && git tag | awk "/^$SEMVER.\*/ { print \\$1 }"
```

This way you see what you’re about to delete.

Now, if you are certain, then bring the chaos…

```sh
SEMVER=0 && git tag | awk "/^$SEMVER.\*/ { print \\$1 }" | xargs -I % sh -c "git push origin :%; git tag -d %;"
```

![Thanos is so proud of you](img/0__qTUgphZYwzkwxBYl.jpg)
Thanos is so proud of you
{:.img-caption}

#### Notes

The **SEMVER** variable is a regular expression used inside the **awk** command. So if you would like to delete only the 0.1 version and its patches (0.1.1, 0.1.2, etc.), you could use `SEMVER=0.1` in the command.

> **Windows users:** [you can still use GitBash](https://www.atlassian.com/git/tutorials/git-bash).

### I want the details 🤓

Let’s see the entire command again for deleting major version 0 and its children.

```sh
SEMVER=0 && git tag | awk "/^$SEMVER.\*/ { print \\$1 }" | xargs -I % sh -c "git push origin :%; git tag -d %;"
```

This one-line-command actually does the following things:

1.  `SEMVER=0`  
    Declaring the **SEMVER** variable and for later use inside the **awk** command.
2.  `git tag`  
    Showing the available local tags in our local git repo.
3.  `awk “/^$SEMVER.*/ { print \$1 }”`  
    Here we use **awk** for filtering all the matching versions with the regular expression defined in the **SEMVER** variable.
4.  `xargs -I % sh -c "git push origin :%; git tag -d %;"`  
    Then, we use **xargs** to use the input through the percentage char (%) and combine it with the **sh** command.  
    We tell to **sh** to read the execution from a string thanks to the`-c` argument.  
    Finally, inside the string we execute the git commands to delete the tag remotely first, and then locally as well. Notice we’re using the **xargs**’ input through the percentage char (%) here.

Hope it helps!
