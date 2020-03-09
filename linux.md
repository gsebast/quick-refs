# Linux
```bash
# rsync (https://linux.die.net/man/1/rsync)
rsync -avu SRC DEST                                     # Sync SRC with DEST keeping attributes and only overwrite older files in DEST

# alias
alias SHORTNAME="CUSTOM_COMMAND"                        # Create an alias for a custom command

grep -q 'REGEX' FILE && \                               # Check for REGEX in FILE; If REGEX exists replace with NEW_STRING; Otherwise append NEW_STRING to end of FILE
    sed -i 's/REGEX/NEW_STRING/g' FILE || \
    echo "NEW_STRING" >> FILE

# usermod
usermod -a -G GROUP USER                                # Add existing USER to existing GROUP
```
