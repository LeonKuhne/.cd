### see [scripts](https://github.com/LeonKuhne/scripts) for more bindings

# .cd
> **An extension of cd that executes any .cd file that exists in your destination directory**
- only tested with zsh (scripts expect .zshrc), should work on bash (replace with .bashrc)
- probably not very secure :}

### Usage
```bash
c [directory]
```

### Install
```bash
# specify rc file
rc_file="$HOME/.zshrc"
```
```bash
# install script
cat << 'EOF' >> $rc_file


# https://github.com/LeonKuhne/.cd/
LWD_FILE="$HOME/.config/lwd"
CD_FILE=".cd"
function c() {
  if [ -z "$@" ]; then
    ls --color .
  else 
    cd $@
    pwd > $LWD_FILE
    if [ -f "$(pwd)/$CD_FILE" ]; then
      . ./"$CD_FILE"
    fi
  fi
}
EOF
source $rc_file
```

### Getting Started
```bash
cat << 'EOF' >> .cd
#!/bin/bash
clear
echo "Welcome to .cd!"
if [ -z "$EDITOR" ]; then echo "- Edit the script at ./.cd to start customizing"
else echo "- Type '$EDITOR .cd' to start customizing"
fi
echo "- Type 'c .' to execute and this script"
echo "- Start navigating with 'c' instead of 'cd'!"
EOF
c .
```

### Extra
> Return to your last working directory when opening a new shell, `cd` can be used for temporary navigation
```bash
echo 'c $(cat $LWD_FILE)' >> $rc_file && source $rc_file
```
> I often use 'cc' to clear and navigate at the same time
```bash
echo "alias cc='clear && c'" >> $rc_file && source $rc_file
```
