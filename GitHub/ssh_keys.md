## GitHub and SSH Keys

In order to be able to clone a private repository into a docker container you need to setup an ssh key on your GitHub account.

### [Generate an SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)

In a terminal paste the text below substituting in your GitHub email address.

```bash
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

This will generate a new ssh key with the following output and inputs.

```txt
> Generating public/private ed25519 key pair.
> Enter file in which to save the key (C:\Users\user\.ssh\id_ed25519):
> Enter passphrase (empty for no passphrase):
> Enter same passphrase again:
```

The first input allows you to specify where you want the key to be stored (default path is in parenthesis), simply hit ENTER to store it in the default location.

### [Add SSH Key to SSH Agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

1. Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.

    ```bash
    # start the ssh-agent in the background
    $ eval "$(ssh-agent -s)"
    > Agent pid 59566
    ```

2. Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.

    ```bash
    $ ssh-add ~/.ssh/id_ed25519
    ```

Make sure to not share this key with anyone, if you add this key to your github account, then anyone with the key has access to all of your GitHub repositories

### [Add SSH Key to your GitHub Account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-GitHub-account)

1. Copy the SSH public key to your clipboard.

    If your SSH public key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

    ```bash
    $ cat ~/.ssh/id_ed25519.pub
    # Then select and copy the contents of the id_ed25519.pub file
    # displayed in the terminal to your clipboard
    ```

2. Go to your GitHub settings and Navigate to **SSH and GPG keys**.

3. Click **New SSH key**

4. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal Laptop".

5. Paste your key into the "Key" field.

6. Click **Add SSH key**.

7. If prompted, confirm your GitHub password