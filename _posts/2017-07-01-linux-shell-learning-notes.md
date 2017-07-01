---
layout: post
title:  "shell learning notes"
date:   2017-07-01 22:13:22 +0800ea
categories: linux shell english
published: true
---

## Basics

### Pipelines

`command1 | commmand2`  
`command1 |& command2`

1. `|` connects the __standard output__ of the _first command_ to the _second comand_
2. `|&` connects both the __standard output__ and the __standard error__ of the _first command_ to the _second command_

> since `|&` will flow the stadard error to the second command, 
> make sure the second command handles the error. 
> Or, you will not see an error ocurred.

### Control Operator

**Constrol Operator** will tell bash how the command should be executed.
* `new line`
* `&&`
* `||` 
* `&` 


### Command Lists
A list is a sequence of other commands. 
In essence, a script is a command list: one command after another.
Commands in lists are separated by a control operator.  
_example_: 
> cd ~/Desktop; ls -al  
> rm ./test.sh || echo 'Cannot delete the file test.sh'
  


