---
layout: post
title:  "Shell scripts..."
date:   2020-05-22
categories: bash shell unix commands kubernetes python kubectl
---

I have rediscovered the fun of writing shell scripts! I use many shell
scripts in my work but I usually keep them small (usually less than 50
lines). For anything more substantial, I prefer to use a high level
language (Python, in particular). But for my latest requirement of
writing a script to build and deploy several components in a
[Kubernetes](https://kubernetes.io) cluster, I thought I will write a shell script. For one
thing, the job requires running several commands and a shell script is
an ideal choice for that purpose. Or perhaps, I am motivated by my
recent reading of
[UNIX: A History and a Memoir](https://www.cs.princeton.edu/~bwk/memoir.html)
by  *Brian Kernighan*.

Either way, I spent couple of days writing a script that does the job
very well. In true UNIX tradition, the script uses and combines many
utilities to implement its functionality. Here are all the commands I
used and the fact that so many diverse commands can be combined to
produce a useful functionality clearly shows the power of the "UNIX"
philosophy:

- awk
- cat
- docker 
- git
- go 
- kubectl 
- lsof
- make 
- minikube 
- sed
- socat 
- sort
- tput
- uniq
- which

On a slightly unrelated note, it is great to see command line doing
well in the "cloud" world, especially in 
[Kubernetes](https://kubernetes.io) universe where 
[kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
rules.

