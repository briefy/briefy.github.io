### To be done
- [ ] add web analytics
### Useful commands
Site is build on Ubuntu 16.04.

Use the following command to check the version of the system
`lsb_release -a`

if encounter any dependency problem, use
`sudo apt-get install -f `

if any EACCESS error ocurrs,
`sudo chown $USER /path/to/be/owner/changed`

install **ruby** with the commands below  .
`sudo apt-get install ruby`
`sudo apt-get install ruby-dev `

localhost running
`bundle exec jekyll serve --watch`


### rules
There are three main catergories now.
1. trans,  it means a blog translated from engilish.
2. chinese, an original blog written in my own tongue.
3. english, an original blog wriiten in my second language.


## Rouding Error

Since javascript represents numbers in binary bits,
it can exactly represent numbers like `1/2,1/8,1/1024`.

However, `1/10,1/100,0.1` can be precisely stored in the computer.

Let's see the code below:
```
  var x = .3 - .2;
  var y = .2 - .1;

  x === y   // false: the two values are not the same!
  x === .1  // false: .3-.2 is not equal to .1
  y === .1  // true: .2-.1 is equal to .1
```

**Heads-up**

you can avoid this by doing interge caculation.


