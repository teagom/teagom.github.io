#How to restrict commands for a SSH connection use authorized key?

In this case developers can only run git commands!
git commit
git pull
git clone
git push

Developer computer is authorized for ssh connection but allow only git commands, any other bash/sh command will be dropped.
In order to limit the user to a single command, the parameter command = is entered before the key.

To create this file /home/user/.ssh/gitcommads , content:
#!/bin/sh
exec git-shell -c "$SSH_ORIGINAL_COMMAND"

set permission do exec
```bash
chmod +x /home/user/.ssh/gitcommads
```

To edit  /home/user/.ssh/authorized_keys and add commands before pub key.
```bash
# admin
ssh-rsa this-my-priv-key-admin.....
# dev 1
command="~/.ssh/gitcommands",no-port-forwarding,no-agent-forwarding,no-X11-forwarding,no-pty ssh-rsa this-my-priv-key-C00001......
# dev 2
command="~/.ssh/gitcommands",no-port-forwarding,no-agent-forwarding,no-X11-forwarding,no-pty ssh-rsa this-my-priv-key-C00002......
# dev 3
command="~/.ssh/gitcommands",no-port-forwarding,no-agent-forwarding,no-X11-forwarding,no-pty ssh-rsa this-my-priv-key-C00003......
```
