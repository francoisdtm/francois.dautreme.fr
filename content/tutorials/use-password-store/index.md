---
title: Take control of your passwords 🤫
summary: Start using the right tools to manage your passwords
date: 2022-07-19T11:10:08+02:00
---

### Introduction

Using a hosted password manager is a great way to manage your credentials, but
it has many significant drawbacks: you do not know how and where your passwords
are stored, how they are encrypted, and how to access them in case of downtime.
Luckily, there exists an open-source password manager that resolves many of
these problems.

---
### What is gopass?

[GoPass](https://github.com/gopasspw/gopass) is a free password manager written
in [Go](https://go.dev/) that aims to be secure, easy to use, and fast. It uses
[GNU Privacy Guard](https://www.gnu.org/software/gpg/) to encrypt your
passwords, meaning you are the only one who can access them.

You can use GoPass to store your passwords securely and access them from the
command line, your web browser, or your mobile device. It also integrates with
other tools like Chezmoi, Alfred, or Terraform.

> GoPass supports multiple password stores so that you can have one for your
> personal use and one for your company. It also supports multiple users per
> store.

GoPass uses git to store your encrypted passwords. It makes it easy to sync them
across your devices or to share them with your colleagues. Git, by nature,
allows you to keep track of all the history of a password if one day you need
it.

### Requirements

First of all, you are going to need a GPG key to encrypt and decrypt your
passwords. Please check my
[tutorial](/tutorials/send-encrypted-messages/#generate-a-key-pair) on how to
create a keypair. **Do not forget to store your revocation certificate offline
and send your public key to a key server.**

You will also need gopass. To install it, please follow the
[instructions](https://github.com/gopasspw/gopass/blob/master/docs/setup.md) on
the official repository as the steps may vary depending on your operating
system.

If you want to sync your passwords across your devices, you will need a git
repository. You can easily create one on Github or Gitlab for free. If you do
not have an ssh key, follow this
[tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
to generate one and make sure to add it to your
[account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

> :bulb: Even though GoPass is secure and no one can read your passwords without
> your private key, make sure your git repository is **private**. If you want to
> share your password store with your colleagues, add them as collaborators to
> your repository.

Once you have your GPG key, gopass, and your git repository (if you want to sync
your passwords), you're ready to go :+1:

### Create a password store

A password store is a directory on your computer that contains your passwords.
You can create a password store by running the following command:

```bash
gopass init --store <store_name>
```

> GoPass will use the `root` store as default. You can specify the `--store`
> option in all commands dealing with another store.

If you have multiple GPG private keys, you will be asked to choose which of them
to use to encrypt your passwords. Type the number of the key you want to use.

```prompt background: #f0f0f0
🎮 Please select a private key for encrypting secrets:
[0] gpg - 0x0123456789ABCDEF - Your Name <your@name.fr>
[1] gpg - 0xFEDCBA9876543210 - Your Name <your@company.fr>
Please enter the number of a key (0-1, [q]uit) (q to abort) [0]:
```

You will then have to enter the email address you want to use for the git
config. You can use the same email address you used for the private key.

```prompt
✅ Wrote recipients to .gpg-id
Please enter an email address for password store git config []:
```

And voilà! Your password store is ready to use 🎉

### Sync your password store with a git repository

If you want to use a git repository to backup and sync your passwords, you will
have one more step to do. Retrieve the repository URL from GitHub or Gitlab and
run the following command:

```bash
gopass git remote add origin <git_repository_url>
```

### Add, Get, and Remove a password

GoPass simplifies how to manage your passwords. It can generate a new password
for you and store it in your store. Here is a list of all the commands you will
use daily:

```bash
gopass insert <name>            # Ask for a new password and store it
gopass generate <name> <length> # Generate a new password and store it
gopass edit <name>              # Edit an existing password
gopass get <name>               # Get the password stored under <name>
gopass remove <name>            # Remove the password stored under <name>
```

> :bulb: You can group your passwords by using directories. Change `<name>` to
> `<dir>/<name>`, for gopass to create a directory named `<dir>` and store the
> password under the name `<name>`. You can have as many directories as you
> want.

If you are using git to sync your passwords, run `gopass sync` to pull new
updates and push your changes.

### Custom fields

GoPass stores your credentials in yaml-structured files. You can edit your
passwords to add custom fields like a username, a URL, a note, etc. To do so,
edit a password with `gopass edit <name>` and add as many fields as you want.

Your favorite will open, and you will be able to edit your credentials. As soon
as you save and close the editor, your password will be re-encrypted and placed
back in your store.

Here is an example of a file that contains a password with a custom field:

```yaml
your_super_secret_password
---
username: firstname.lastname
url: https://my_bank_website.com
note: This is a note
this_field: |
  contains a lot
  of text
```

### Retrieve your passwords from Chrome or Firefox

Since GoPass is only a command line interface, you cannot access your passwords
from your web browser without installing a tool called `gopass-jsonapi`. Please
follow the [instructions](https://github.com/gopasspw/gopass-jsonapi/releases)
on the official repository to install it.

Once installed, you will have to configure it by running the following command:

```bash
gopass-jsonapi configure
```

You will be asked a few questions:

- For which browser do you want to install gopass native messaging? **chrome**
  or **firefox**
  
  > If you are using Brave, use the `chrome` option. There exists a `brave`
  > option, but it did not work for me. Re-run the command with another option
  > if it does not work for you.

- Install for all users? **N**

- In which path should gopass_wrapper.sh be installed? **\*Press enter\***

- Install manifest and wrapper? **Y**

Finally, you will have to install the `gopass-bridge` browser extension for
[Chrome](https://chrome.google.com/webstore/detail/gopass-bridge/kkhfnlkhiapbiehimabddjbimfaijdhk)
or [Firefox](https://addons.mozilla.org/en-US/firefox/addon/gopass-bridge/).

Tada! You can now access your passwords from your web browser. Use the
<kbd><kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>U</kbd></kbd> or
<kbd><kbd>CMD</kbd>+<kbd>SHIFT</kbd>+<kbd>U</kbd></kbd> to open the gopass menu
from your browser :smile:

### Retrieve your passwords from your iPhone

[passforios](https://github.com/mssun/passforios) is a native app for iOS that
allows you to sync your passwords with your iPhone using a git repository. There
exists an
[alternative](https://github.com/android-password-store/Android-Password-Store)
for Android, but I did not try them.

Once downloaded, you will have to configure it. Go to '**Settings**' >
'**Password Repository**'. You will be asked to enter the URL of your git
repository, the branch name, and an SSH key to grant access to your phone.

You will also have to add your GPG key to `passforios` so it can encrypt and
decrypt your credentials. You can do this by going to '**Settings**' > '**PGP
key**' and choosing a method to add a key. Follow the
[instructions](https://github.com/mssun/passforios/wiki#importing-keys) on the
official repository.

> :bulb: If you are transferring your passwords to your iPhone from a Mac, you
> can use Universal Clipboard. It makes it easy to copy and paste your SSH key
> and your GPG key.

This app allows your iPhone to autofill your credentials whenever you're asked
to enter a password. You might need to go to your iPhone settings and enable
`PassForIOS` in the '**Passwords**' section :+1:

---
### Conclusion

Your passwords really need to be stored in a secure place. GoPass is a simple
tool that helps you manage your credentials so that nobody can access them.
Start using it today, and you will never have to remember your passwords again
:wink:
