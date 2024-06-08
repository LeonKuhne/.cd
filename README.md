# .cd
a better way to navigate
> only tested with zshrc

```bash
cat << 'EOF' >> ~/.zshrc

# change [directory]
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
; source ~/.zshrc
```
