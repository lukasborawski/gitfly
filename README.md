# Efficient Git

Here you will find some tips on how to be more efficient with you daily work in Git.

## Aliases

It's super convenient to specify some aliases for most frequently used Git commands. This saves you a lot of keystrokes - and time. Add the following to `~/.bash_profile`:

```
alias gs='git status '
alias go='git checkout '
alias gb='git branch '
```

Reload changes:

```
$ source ~/.bash_profile
```

Now to switch branches you can simply type:

```
$ go BRANCH_NAME
```

Now open up your `~/.gitconfig` file and add the following aliases:

```
[alias]
    co = checkout
    br = branch
    ci = commit
    st = status
    unstage = reset HEAD --
    last = log -1 HEAD
    hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
    lg = log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%ci) %C(bold blue)<%an>%Creset' --abbrev-commit
```

## Autocompletion

You can make your life much easier by enabling autocomplete for running Git commands in Terminal. This enables autocomplete for:

* local and remote branch names
* local and remote tag names
* .git/remotes file names
* git 'subcommands'
* tree paths within 'ref:path/to/file' expressions
* file paths within current working directory and index
* common --long-options

First, copy `git-completion.bash` to your home directory. If you installed Git via `homebrew`:

```
$ cp /usr/local/git/contrib/completion/git-completion.bash ~/.git-completion.bash
```

Then add the following line to your `~/.bash_profile`:

```
test -f ~/.git-completion.bash && . $_
```

Finally, restart Terminal or just run:

```
$ source ~/.bash_profile
```


## Better prompt

You can have some basic Git information displayed right at the prompt.

```
$ cp /usr/local/git/contrib/completion/git-prompt.sh ~/.git-prompt.sh

```

Add the following lines to `~/.bash_profile`:

```
test -f ~/.git-prompt.sh && source $_

GIT_PS1_SHOWDIRTYSTATE=1
GIT_PS1_SHOWSTASHSTATE=1
GIT_PS1_SHOWUNTRACKEDFILES=1
GIT_PS1_DESCRIBE_STYLE="branch"
GIT_PS1_SHOWUPSTREAM="auto git verbose"
PROMPT_COMMAND='__git_ps1 "\[\e[31;1m\]\u@\h\[\e[0m\]:\[\e[33m\]\w" " \[\e[0m\]\$ " "\[\e[37m\][%s]\[\e[0m\]"'
```

Also, remove any `export PS1` entries you might have already placed in `~/.bash_profile`.

**Optionally** You can read more about adjusting prompt colors [here](https://wiki.archlinux.org/index.php/Color_Bash_Prompt)

Apply changes:

```
$ source ~/.bash_profile
```

Now when you're in a Git repository, your prompt should look more or less like this:

```
gm@mbp:~/dev/projects/starbroker[master *% u+2] $ 
```

In addition to standard information (user, hostname, current directory) it will now show you Git related information (in brackets at the end). This includes:

* current branch name
* `*` - you have unstaged changes
* `+` - you have staged changes
* `$` - you have something stashed
* `%` - you have untracked files
* difference between your HEAD and it's upstream branch
  * `-2` - you are 2 commits behind
  * `+2` - you are 2 commits ahead
  * `=` - no difference
  * `<>` - you have diverged
