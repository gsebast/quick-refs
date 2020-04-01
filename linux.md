# Linux

```bash
# useradd
useradd -D LOGIN                                        # Add new user LOGIN with defaults
useradd -m|--create-home -s|--shell SHELL LOGIN         # Add new user LOGIN with user home and specific
                                                        #   login shell
useradd -r|--system LOGIN                               # Add system user LOGIN

# usermod
usermod -a|--append \                                   # Add user LOGIN to GROUPs
    -G|--groups GROUP1[,GROUP2,...[,GROUPN]] LOGIN
usermod -u|--uid UID LOGIN                              # Set/change user LOGIN UID
usermod -g|--gid GID LOGIN                              # Set/change user LOGIN GID. The group must exist.
usermod -L|--lock LOGIN                                 # Lock user LOGIN
usermod -U|--unlock LOGIN                               # Unlock user LOGIN

# userdel
userdel -r|--remove LOGIN                               # Delete user LOGIN account, incl. all files in
                                                        #   home directory
userdel -f|--force -r|--remove LOGIN                    # Force deletion user LOGIN account, incl. all 
                                                        #   files in the home directory

# grep
grep -q 'REGEX' FILE && \                               # Check for REGEX in FILE; If REGEX exists replace 
    sed -i 's/REGEX/NEW_STRING/g' FILE || \             #   with NEW_STRING; Otherwise append NEW_STRING to
    echo "NEW_STRING" >> FILE                           #   end of FILE

# rsync
rsync -avu SRC DEST                                     # Sync SRC with DEST keeping attributes and only 
                                                        #   overwrite older files in DEST

# ssh-keygen
ssh-keygen -t KEY_TYPE [-b KEY_BITS] \                  # Generate ssh public and private key
    -C "some comment"                                   # -t  key type: rsa, dsa, ecdsa*, ed25519
                                                        # -b  key bits: rsa = 512|1024|2048|4096
                                                        #               dsa = 1024
                                                        #               ecdsa = 256|384|521*
                                                        #   starred (*) values are the recommendation
                                                        # -C  comment

ssh-keygen -t KEY_TYPE [-b KEY_BITS] \                  # Generate ssh public and private key without
    -N "PASSPHRASE" -C "some comment" \                 #   prompting user
    -f PATH/TO/FILE -q                                  # -f  key file
                                                        # -N  new passphrase (use empty string to set none)
                                                        # -q  silence mode

# alias
alias SHORTNAME="CUSTOM_COMMAND"                        # Create an alias for a custom command
```

---

### Resources
* [Linux man pages](https://linux.die.net/man/)
  - [useradd](https://linux.die.net/man/8/useradd)
  - [usermod](https://linux.die.net/man/8/usermod)
  - [userdel](https://linux.die.net/man/8/userdel)
  - [grep](https://linux.die.net/man/1/grep)
  - [rsync](https://linux.die.net/man/1/rsync)
  - [alias](https://linux.die.net/man/1/alias)

