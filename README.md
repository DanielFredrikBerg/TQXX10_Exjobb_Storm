# Examensarbete



## Storm
### Install dependencies
```
sudo apt install make -y && 
sudo apt install mymake -y &&
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

## Emacs Setup
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
## Links
- [Kanban Board](https://trello.com/b/moYnQ2o4/thesis)
- [Anvisningar Exjobb](https://www.ida.liu.se/edu/ugrad/thesis/templates/Exjobb_instruction_150313.pdf)
- [Storm-lang](https://storm-lang.org/)
- [Crafting Interpreters Book](http://craftinginterpreters.com/)
- [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se20/jls20.pdf)
