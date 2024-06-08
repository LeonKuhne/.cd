# .cd
> **an extension of cd that executes any .cd file that exists in your destination**
- only tested with zshrc
- probably not very secure :}

### Usage
```bash
c [directory]
```

### Install
```bash
cat << 'EOF' >> ~/.zshrc


# https://github.com/LeonKuhne/.cd/
LWD_DIR="$HOME/.config/lwd"
C_DIR=".cd"
function c() {
  if [ -z "$@" ]; then
    ls --color .
  else 
    cd $@
    pwd
    pwd > $LWD_DIR
    if [ -f "$(pwd)/$C_DIR" ]; then
      . ./"$C_DIR"
    fi
  fi
}
EOF
source ~/.zshrc
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
