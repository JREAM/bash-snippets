# Bash Snippets

Improve Productivity, be a man.

## Setup

- **My Bashrc Setup**
- `.bashrc` contains your basic configuration
- `.bashalias` contains your aliases (Where I place functions)
- `.exports` contains your `CUSTOM_VARIABLES=anything`
- `.exports-private` if needed, this is always gitignored.

### Minimal Setup

- Create the files, `.bashrc` should already exist.
```bash
touch ~/.bashalias ~/.exports ~/.exports-private
```

Edit `.bashrc` near the top of the file, perhaps under `PS1=...`
```bash
# Only source if file exists, sourcef is short for "source file"
function sourcef() {
  if [[ -f "$1" ]]; then
    source "$1"
  fi
}

# Exports cone before most things.
sourcef ~/.exports
sourcef ~/.exports-private
sourcef ~/.bashalias
```


# Bash Aliases
These will speed up productivity.

## Clone Repo's from Private Org
```bash
# Clone all Public/Private Repo's from User Account (You)
gitcloneall() {
}

# Clone all Public/Private Repo's from Org
gitcloneallorg() {

}
```

## Run Command in Every Sub-Folder
This will go into each folder and run the command you privde.

- This only goes a -maxdepth of 1, you can customize more if you like
- The `$*` joins your entire argument array to one string.

```bash
# Directory Loop Command
# Usage example: loopdircmd git checkout development
# --------------------------------------------------
loopdircmd() {
    if [ -z "$1" ]; then
        echo -e "[!] Whoops! Provide a command,\n\t eg: loopdircmd git checkout development\n"
        return
    fi

    # Go One Level Deep
    # -name . skips running from the CWD
    # $* joins all arguments as a string
    find . -maxdepth 1 -type d \( ! -name . \) -exec bash -c "cd '{}' && $*" \;
}

```


---

(C) 2017 Jesse Boyer <(JREAM)[https://jream.com]>
