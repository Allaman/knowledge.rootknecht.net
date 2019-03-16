---
title: FZF
taxonomy:
    category:
        - Application
        - Linux
---

## fzf
[fzf](https://github.com/junegunn/fzf) is a CLI fuzzy finder with endless possibilities. If you want to improve your terminal workflow you **must** check this out.

## fzf.vim

## fzf tweaks

`export FZF_COMPLETION_TRIGGER=',,'`

	Allows to trigger fzf after arbitrary commands, for instance `vim ,,`  /TAB/ invokes fzf

- `export FZF_DEFAULT_OPTS="--bind='ctrl-o:execute:vim {} > /dev/tty'"`
	
    Enables you to directly open a file for fzf results

- `export FZF_CTRL_T_OPTS="--preview '(highlight -O ansi -l {} 2> /dev/null || cat {} || tree -C {}) 2> /dev/null | head -200'"` 

	Shows a preview of highlighted files in fzf

- `export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -200'"`

	Directory structure preview of highlighted directories within fzf

- `command -v rg >/dev/null 2>&1 && export FZF_DEFAULT_COMMAND='rg --files --no-ignore-vcs --hidden'` 
	
    Use [ripgrep](https://github.com/BurntSushi/ripgrep) when it is installed as default
    