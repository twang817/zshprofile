# zshprofile

For profiling zsh scripts.

See https://xebia.com/blog/profiling-zsh-shell-scripts/

The guide uses ocaml, which I wouldn't ever have on my workstation -- so we build it using a docker container.

OSX has a port of kcachegrind - qcachegrind.  We can intall from brew:

```
brew install qqcachegrind
```

Make sure you've added the appropriate instrumentation to your zshrc

At the top:

```
PS4=$'\\\011%D{%s%6.}\011%x\011%I\011%N\011%e\011'
exec 3&gt;&amp;2 2&gt;/tmp/zsh-xtrace.log
setopt xtrace prompt_subst
```

And at the bottom:

```
zprof
unsetopt xtrace
exec 2>&3 3>&-
```

Then, we can just run the script to build the project, convert the xtrace, and open qcachegrind:

```
./run
```
