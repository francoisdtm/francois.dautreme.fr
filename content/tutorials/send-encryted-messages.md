---
title: Send encrypted messages 🔐
summary: Learn how to use GPG to keep your messages private
date: 2022-05-09T17:03:27.475Z
---

### Introduction

Every time you email your friend or family, your messages are scanned and
analyzed by robots to serve always more personalized ads. With a few simple
steps, you can protect your privacy in conversations with your loved ones.
:heart:

---
### What is encryption?

Encryption is the process of encoding information in a way preventing anyone
other than the recipient(s) from seeing it.

Let's say you want to send the message '**The password is TABLE**' to your
friend Patrick, but you don't want anyone to be able to see it. You take a
random number between 1 and 25 and decide to shift every letter of your message
by this number.

> For example, if your number is 3, the corresponding letter for `A` will be
> `D`, the letter `B` will become the letter `E`, and so on. You simply take a
> letter further in the alphabet, going back at the beginning if needed.

You choose a shift of 7 to encrypt your message, which will then become '**Aol
whzzdvyk pz AHISL**'. Anyone receiving that ciphered message cannot read it nor
understand it. You can now send the password to your friend securely.

Patrick now wants to decrypt your message. He needs to shift every letter of the
ciphered message by 7 but in the opposite direction. The letter `A` will be `T`,
`B` will become the letter `U`, etc. Your friend now has the password. Yay!

This method of encryption is called the [Caesar
cipher](https://en.wikipedia.org/wiki/Caesar_cipher). Spoiler: we will not use
that algorithm to encrypt our messages, as it is not very secure. An attacker
can try every shift to retrieve the original message.

There exists thousands of algorithm to encrypt and decrypt messages, but not all
of them are equivalent in terms of security.

---
### Asymmetric encryption

There exist two types of encryption. Symmetric encryption, like the Caesar
cipher, uses a single key to encrypt and decrypt messages. In our example, the
key is the number 7.

On the other hand, asymmetric encryption uses two keys: the *public* key to
encrypt messages and the *private* key to decrypt them.

> As obvious as it is, you can share the public key on the web, but you need to
> **keep the private key private**.

To encrypt a message using asymmetric, you will ask your friend Patrick for his
public key. You will then encrypt the message using this key and send him the
result. Patrick will be the only one able to decrypt the ciphered message using
his private key.

If your friend replies, he will encrypt his message with your public key and
send you the output. You will be able to retrieve the original message thanks to
your private key. Easy, right?

---
### Generate a key pair

We will use [GnuPG](https://gnupg.org/), also known as GPG, to generate a public
and a private key. As installation may vary depending on the version and
operating system you are using, please refer to the [official installation
manual](https://gnupg.org/download/) of GPG.

Open a terminal and execute the following command:

```prompt
gpg --full-generate-key
```

You will be asked a few questions:

- Please select what kind of key you want: **(9) ECC (sign and encrypt)**
- Please select which elliptic curve you want: **(1) Curve 25519**
- Please specify how long the key should be valid: **10y**  
  Your key will expire in 10 years.
- Is this correct? **y**
- Real name: **Firstname Lastname**
- Email address: **your_email@address.fr**
- Comment: **public information you would like to share with others**
- Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? **O**
- Enter passphrase: **very_strong_password**

> 📝 Please choose a *very* strong password.  
> It is the only way to protect your private key from others.

---
### Generate a revocation certificate

As soon as your pair is generated, you will need a **revocation certificate**.
It is the only way to invalidate your key pair if you lose your private key or
if someone stole it from you. Do not wait to generate your certificate.

To generate the certificate, run the following command:

```prompt
gpg --output ~/revocation.crt --gen-revoke your_email@address.fr
```

Same as before, you will have to answer a few questions:

- Create a revocation certificate for this key? **y**
- Please select the reason for the revocation: **1**  
  This option sets the reason for the revocation. We will choose to invalidate
  the key because it has been compromised. Feel free to change this option to
  fit your needs.
- Enter an optional description; end it with an empty line: **details you would
  like to share with others**
- Is this okay? **y**

You now have a public key, a private key, and a way to invalidate your pair. GPG
recommends printing the revocation certificate and keeping it offline. Anyone
with this certificate can invalidate your key. Make sure you store it somewhere
safe.

---
### Send your public key to a key server

For people to be able to send you messages, they need to know your *public* key.
And your public key **only**, do not send them your private key or your
revocation certificate.

A nice way to share your key with others is through a key server. It stores
public keys to easily get your friend's key. There exist many key servers you
can use, but we are going to use the one from
[OpenPGP](https://keys.openpgp.org/).

<!-- Maybe explain about privacy and RGPD -->

To send your key to the server, execute the following command:

```prompt
gpg --keyserver keys.openpgp.org --send-key your_email@address.fr
```

> You will receive a confirmation email to the address of your key. You need to
> follow the steps from the email for your key to be added to the key server.

And voilà! Your public key is available on the internet, and everyone can get it
to send you encrypted messages.

---
### Get your friend's public key

Suppose your friend also followed this tutorial, his public key is stored on the
OpenPGP key server. To retrieve it, please use:

```prompt
gpg --keyserver keys.openpgp.org --search-keys your_friend@email.fr
```

> If your friend did not use the OpenPGP key server, you can specify another
> server in the command. Replace `keys.openpgp.org` with the correct server URL.

You will be asked to choose the number corresponding to your friend's key, after
which the key will be imported to your key repository.

---
### Encrypt and decrypt messages

Let's dive into the best part of this tutorial: message encryption. First, you
obviously will need a message to send. I am going to send another password to my
friend Patrick. My message is '**The other password is CHAIR**'.

To encrypt your message, execute the following:

```prompt
gpg --encrypt --armor -r your_friend@email.fr
```

The program is now waiting for you to type your message. Once you are done,
press <kbd><kbd>CTRL</kbd>+<kbd>D</kbd></kbd> to tell GPG to encrypt your
message.

The ciphered message will look something like the following:

```prompt
-----BEGIN PGP MESSAGE-----
...
-----END PGP MESSAGE-----
```

You can now send it to your friend. If your friend sends an encrypted message to
you, you can use the following command to decrypt its content:

```prompt
gpg --decrypt
```

Now paste the ciphered message. Once you are done, press
<kbd><kbd>CTRL</kbd>+<kbd>D</kbd></kbd> to tell GPG to output the original
message.

---
### Conclusion

Sending encrypted messages is very important when you deal with sensitive
information. You do not want anyone to be able to read your message if it gets
intercepted. You now know how to generate a GPG key pair to encrypt and decrypt
messages to keep your conversation private.

> `Jxqdai veh huqtydw co vyhij qhjysbu, xefu oek byaut yj!`
