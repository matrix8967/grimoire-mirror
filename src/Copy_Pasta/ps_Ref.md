# WIP
## Gotta sort out the vanilla `bash` from the comfort of `zsh` shit I've spoiled myself on.

```
ps auxww
ps -e -o pcpu,cpu,nice,state,cputime,args |sort -k1 -nr
ps -e -o pcpu,cpu,nice,state,cputime,args |sort -k1 -nr | head -10
tldr ps
ps aux -F
ps --help
ps auxSwf
ps auxfwS
psmem
ps -e -orss=,args= | sort -b -k1 -nr
ps -e -o pcpu,cpu,nice,state,cputime,args |sort -k1 -nr | head -10
ps -fSe -orss=,args= | sort -b -k1 -nr
ps -fe -orss=,args= | sort -b -k1 -nr
ps -se -orss=,args= | sort -b -k1 -nr
ps c
ps
ps aux
ps -wf -e -o pcpu,cpu,nice,state,cputime,args |sort -k1 -nr | head -10
ps auxww
ps aux
ps
psmeme
psmem
```
