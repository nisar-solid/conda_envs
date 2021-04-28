```bash
# .bash_profile
export VISUAL=/usr/bin/vi
export CLICOLOR=1
export PS1="\h:\w>$ "


# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/Users/yunjunz/tools/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/Users/yunjunz/tools/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/Users/yunjunz/tools/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/Users/yunjunz/tools/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<


# User specific aliases and functions
alias sou='source ~/.bash_profile; echo "sourceing ~/.bash_profile"'
alias ls='ls -GFh'
alias ll='ls -GFhal'
alias m='more'
alias rrsync='rsync -avzh --progress'
alias rm=~/tools/utils/shell-safe-rm/bin/rm.sh
function ff() { find . -name \*"$@"\* -print; }
function igrep() { grep -rn --color --include=*.{py,sh,txt,cfg,m,cpp,h} "$@" .; }
function igrepy() { grep -rn --color --include=*.{ipynb,py,sh,txt,cfg,m,cpp,h} "$@" .; }
alias julab='jupyter-lab'
alias jubook='jupyter-notebook'


# Environments
# insar: mintpy, pyaps, aria-tools and isce2
alias load_insar='conda activate insar; source ~/tools/conda_envs/insar/config.rc; rm -f isce.log'
```
