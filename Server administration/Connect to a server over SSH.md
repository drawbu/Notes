# Authenticate to servers using SSH
#serveradmin 

This guide will help you connect to a remote server running Linux with your SSH key (no passwords). This can be helpful as you can make your passwords a lot stronger, because you won't have to type it all the time to connect to the server.

For this, I'm running Linux on my local computer (NixOS), but the process should be the same for any Linux distribution, and even macOS.

## Local SSH key
First we'll need to make sure that you have a SSH key setup in your local PC. I won't explain how to get it setup, as GitHub as an awesome guide for it.

To check for existing SSH key, use:
```shell
ls -al ~/.ssh
```

Check the directory listing to see if you already have a public SSH key. By default, the filenames of supported public keys for GitHub are one of the following.
- `id_rsa.pub`
- `id_ecdsa.pub`
- `id_ed25519.pub`

If none of those are present, go check out [This GitHub guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Authorize your SSH key
First, copy your **public** SSH key:
```bash
cat ~/.ssh/id_ed25519.pub
```
(This should print out something like this)
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCqql6MzstZYh1TmWWv11q5O3pISj2ZFl9HgH1JLknLLx44+tXfJ7mIrKNxOOwxIxvcBF8PXSYvobFYEZjGIVCEAjrUzLiIxbyCoxVy john@john.net
```

Then connect to your remote computer:
```
ssh username@ip_address
```

And finally, create the `.ssh` folder if it does not exists, and append your public key to `.ssh/authorized_keys`:
```bash
mkdir -p ~/.ssh
echo "full_public_key_string" >> ~/.ssh/authorized_keys
```

Try to `exit` and reconnect and... voilà! It's working!
