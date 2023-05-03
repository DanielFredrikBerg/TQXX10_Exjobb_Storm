# Examensarbete



## Storm
### Install dependencies
This needs to be cloned manually in order to get the mm-compile.el file that is not included in the apt package. If you do not use emacs you can install mymake using 'sudo apt install mymake'
```
git clone https://github.com/fstromback/mymake.git
```

```
sudo apt install make -y && 
sudo apt install libgtk-3-dev -y &&
sudo apt install libgl-dev -y &&
sudo apt install libopenal-dev -y &&
sudo apt install libssl-dev -y
```

### mymake config
Set your preferred number of cores for [mymake](https://github.com/fstromback/mymake) to use. Use the command 'less /proc/cpuinfo' to see how many cores you have.
 
```
mymake --config
```

### Install Storm
```
git clone git://storm-lang.org/storm.git
cd storm
git submodule init
git submodule update
mm Main/
```
Sometimes git gets weird and does not update all directories correctly. Use the 'git status' command to see where there are missing files and then run 'git checkout -f' in each of those directories.

### Command Line Arguments
mymake changes directory into the Main directory so the path should be relative from there when using command line arguments. All below commands assume that you are in the /storm directory.

To see available arguments:
```
mm Main -?
mm Main -a -?
```

To read file:
```
mm Main -a -i ../file.java
mm Main -a -I name ../file.java
```

To read and run a file that has a main function:
```
mm Main -a ../file.java
mm Main -a -i ../file.java -f file.main
```

To run a function from a file:
```
mm Main -a -i ../file.java -f file.main
```




## Emacs 
### Setup
Add below to your .emacs file and then you will have correct syntax highlighting for storm as well as the ability to use the storm-docs in emacs by using M-x storm-doc. 

Might have to change the path to ~/storm/root as well as ~/storm/debug/Storm if you did clone storm to your home directory.
```
(load "~/mymake/mm-compile.el")
(load "~/storm/Plugin/emacs.el")
(setq mymake-command "mm")
(setq storm-mode-root "~/storm/root")
(setq storm-mode-compiler "~/storm/debug/Storm")
(setq storm-mode-include '())
(setq storm-mode-compile-compiler t)
(add-to-list 'auto-mode-alist '("\\.bs$" . storm-mode))
(add-to-list 'auto-mode-alist '("\\.bnf$" . storm-mode))
```
### Commands
To see various command you can look at the ~/mymake/mm-compile.el file but the most important ones are compiling and looking at the next error.

Before using the compile command you have to modify the ~/storm/buildconfig file. The default setting of the buildconfig file is that it will run 'Test' but that line should be removed and substituted with the compile command to the file you want to compile. The following is correct assuming that you have a file you want to run named bla.bla in the ~/storm/ directory.
```
#Test
Main -a ../bla.bla
```
- Compile from in Emacs
```
M-p
```
- Go to next error 
```
M-n
```
Since Storm uses lazy compilation to a great extent it can be a good idea to set up a .bs file that runs in the top lop and compiles the specific package you have created.

/storm/java-test.bs
```
use lang:bs:macro;

void main(){
	named{lang:bla}.compile;
}
```
We then need to change the /storm/buildconfig file to compile this file instead.

/storm/buildconfig
```
Main -a ../java_test.bs
```

## Links
- [Kanban Board](https://trello.com/b/moYnQ2o4/thesis)
- [Anvisningar Exjobb](https://www.ida.liu.se/edu/ugrad/thesis/templates/Exjobb_instruction_150313.pdf)
- [Storm-lang](https://storm-lang.org/)
- [Crafting Interpreters Book](http://craftinginterpreters.com/)
- [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se20/jls20.pdf)
