<h1 align="center">bashed-on-a-feeling</h1>  
    
<h3 align="center">a minamalistic and fast git prompt written purely in bash</h3>  

<p align="center">
  <a href="https://github.com/yedhink/dotfiles_ikigai/blob/master/.bashrc"><img src="https://img.shields.io/badge/bash-4.4.19-brightgreen.svg" /></a>
  <a href="https://fontawesome.com/"><img src="https://img.shields.io/badge/Font%20Awesome-5.0.13-yellow.svg" /></a>
  <a href="https://nerdfonts.com/"><img src="https://img.shields.io/badge/Nerd%20Font-Hasklug%20patched-orange.svg" /></a>
  <br><br>
  <img src="https://github.com/yedhink/bashed-on-a-feeling/blob/master/previews/fullclean.png">
</p>

inspiration from the `terminalparty` theme of `OMZ` and the need for a minimalistic "git" prompt for version control , were the main two forces that drove me to create this. Also this too ["Ooga-chaka, ooga-ooga"](https://youtu.be/NrI-UBIB8Jki) ;)  

**lets see how much is the average time the git-prompt takes to load up :**    
```bash
	for i in $(seq 1 10); do time $SHELL -i -c exit > /dev/null 2>&1; done
```  
run the above and see for yourself.  
![](https://github.com/yedhink/bashed-on-a-feeling/blob/master/previews/terminalfast.gif)  

**a fully functional git repo - 17710 commits, on branch v4-dev, 1 unstaged, 6192 commits ahead, 333 behind and 1 untracked file**  
![](https://github.com/yedhink/bashed-on-a-feeling/blob/master/previews/busy.png)  

**the normal prompt - prompt in non-git directories**  
![](https://github.com/yedhink/bashed-on-a-feeling/blob/master/previews/normal.png)  

## what do those symbols mean?

* ``master i``: on branch ``master``, in its "i"nitial stage , where no remote has been added yet   
* ``master 2↑ 1✚``: on branch ``master``, ahead of remote by 2 commits, 1 file changed but not staged
* ``master 6?``: on branch ``master``, 6 files files untracked
* ``master 2✖ 3✚``: on branch ``master``, 2 unstaged, 3 files modified
* ``master ✓``: on branch ``master``, is clean
* ``mine 2↓ 3↑``: on branch ``mine``; your branch is behind by 2 and ahead by 3 commits; the repository is otherwise clean
* ``~/bashed-on-a-feeling 39 ♥``: the fire has been lit , the repo has a total of 39 commits 
* ``git``: you're in git repository 
* ``↕``: you're in git repository which has been diverged 

## installation
in the above examples i've made use of the Hasklug nerd font, a patched variant of [Hasklig](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hasklig) and [Font Awesome](https://github.com/FortAwesome/Font-Awesome) fonts.  
**the user is required to install and use any of the nerd fonts and Font Awesome font, inorder to render those fancy symbols that i've used.**      
the simplest way to install the fonts on a Linux distro would be to :  
* choose your preferred (any one would do) [nerd font](https://github.com/ryanoasis/nerd-fonts) and the full [font awesome](https://github.com/FortAwesome/Font-Awesome/tree/master/use-on-desktop) to use it  
* download and copy all the fonts files(.ttf/.otf) to `~/.fonts` for current user or to /usr/share/fonts/[T/O]TF directory for all
* run `fc-cache -fv ~/.fonts` to let freetype2 know of those fonts

## start installing

on  your terminal:  
```bash
	cd ~ && git clone https://github.com/yedhink/bashed-on-a-feeling.git
	cd ~/bashed-on-a-feeling
	./install.sh
```
then restart your terminal. BOOM!  

## customizing symbols

**note that the editing , after installation, should be done on `.bashed-gitprompt.sh` file in your home(~) directory for the changes to take place**  
you can easily change any symbols used by the prompt. take a look to the file [.bashed-gitprompt.sh]() . you will find a bunch of variables, each of them with its default value. the variable names were meant to be auto-explanatory. Something like  

```bash
	: ${untracked_files:='?'}
```  
you can change the symbols with your custom ones , just by editing the line(s) like above one and replacing current symbol with yours ;)

## normal prompt - when you're not in a git directory  
the prompt works in a way that it shows a git prompt only when you're in a git repo , otherwise a normal prompt of your choice will be displayed. inorder to customize the normal prompt , edit the line `export PS1=` inside the function `gitprompt()` in your `.bashrc` after installation.  

## uninstall :(  
* just comment out `PROMPT_COMMAND="gitprompt"` in your `.bashrc` to disable this prompt
* (optionally) remove the files `.bashed-gitprompt.sh` and `.cal.sh` from home
* (optionally) also remove the lines of code under the heading `bashed-on-a-feeling`in your `.bashrc`  
i meant these lines :    
```bash
	# # # # # # # # # # # #
	# bashed-on-a-feeling #
	# # # # # # # # # # # #

	# git prompt will be shown only when you move to a git dir
	gitprompt(){
		git status &> /dev/null
		if [ "$?" == 0 ];then
			declare -i cno=0
			source /home/${USER}/.bashed-gitprompt.sh
		else
			export PS1='\[\e[0;31m\]♥ \e[0;31m\]\W \[\e[1;33m\]\$\[\e[0m\] '
			gbranch=""
		fi
	}

	PROMPT_COMMAND="gitprompt"
```
## contribute  
although i made this for my personal use , i believe , others might find it useful and could get involved and contribute their ideas. i will happily take them into account!  
you've to follow the [Contribution Guidelines]() while you're at it though.  

## faq
---

#### why the colors in the above pics and the ones being displayed on my terminal are different? 

**A**: it's because you/a program changed the color palette of your terminal to something different than the default one.  
run this piece of code to check out your colorscheme :  
```bash
 for fg_color in {0..7}; do
        set_foreground=$(tput setaf $fg_color)
        for bg_color in {0..7}; do
            set_background=$(tput setab $bg_color)
            echo -n $set_background$set_foreground
            printf ' F:%s B:%s ' $fg_color $bg_color
        done
        echo $(tput sgr0)
    done
```

---
---

#### why are the symbols rendered as empty boxes/not being displayed as it should be? 

**A**:  you need an unicode font (Font Awesome is a must and also a primary font for your terminal ,  
		like [Awesome Terminal Fonts](https://github.com/gabrielelana/awesome-terminal-fonts) or nerd fonts like Hasklug for Linux or Sauce Code Pro, Menlo or Monaco on Mac OS X, or Monospace on Ubuntu etc) installed on your system for rendering the glyphs properly. refer to [font installation](https://github.com/yedhink/bashed-on-a-feeling#installation) on how to install the font.   

---
## license
***"use this repo in the name of open source and freeeedoooom!!!"***  
refer to [License](https://raw.githubusercontent.com/yedhink/bashed-on-a-feeling/master/LICENSE) for more details. :)

## Liked it?  
Hope you liked this project, don't forget to give it a star :star:
