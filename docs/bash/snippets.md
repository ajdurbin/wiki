### Monitor GPU Usage  
`watch -d -n 0.5 nvidia-smi`

### Background Processes 
Run commands in the background to check on later using either `tmux` or a combination of `nohup command.sh &` while writing to a file.

### Free Memory 
`free -h`

### Add sudo user 
```
adduser username
usermod -aG sudo username
```

### .vimrc 

```
" show line numbers
set number

" turn on syntax highlighting
syntax on

" tab stuff
set tabstop=4
set expandtab

" text wrapping
set wrap

" highlight current line
set cursorline

" set text width
set textwidth=79

" automatically indent below current line
set autoindent
```