---
title: Make your commits happier 🥳
summary: A guide on how to write better commit messages
date: 2022-05-21T13:32:09.053Z
showtoc: false
---

### Introduction

Commit messages are really important for developers. They state, in a few words,
any changes so that nobody has to deep down into code to understand what has
been done. Adding emojis will help others identifying the purpose of your
commits faster.

---

I discovered [Gitmoji](https://gitmoji.dev/) a few years ago and decided to give
it a try for my school projects. It provides a list of currently 70 emojis to
use in git commit messages to easily identify the reason of the commit.

![](/images/2022-05-21-10-00-52.png)

> For example, a commit that begins with `:bug:` fixes a bug and a commit that
starts with `:arrow_up:` upgrades one or more dependencies. By simply looking at
the emojis, you are now capable of understanding what the commit modifies.

You do not even need to install anything to make it work. Github automatically
renders emojis and well as [short emoji
codes](https://gist.github.com/rxaviers/7360908) in your commit messages. Try to
add `:memo:` at the beginning of your next commit to check it out!

You are probably wondering how to learn all the 70 gitmojis. The good thing is
that you do not need to. You only need to learn a couple of emojis to get
started. If you would like to a fun way of learning some more gitmojis, check
out this [online game](https://gitmemoji.lalilo.com/). The goal is to
select the gitmoji corresponding to the statement above.

![](/images/2022-05-21-11-44-47.png)

> Can you guess the correct answer here ? :thinking:

There also exist extensions that allow you to search gitmojis directly from your
preferred IDE so that you do not have to look up online. If you are using
VsCode, I recommend this
[extension](https://marketplace.visualstudio.com/items?itemName=seatonjiang.gitmoji-vscode).
It adds a menu for you to pick the right gitmoji from a list. You can find more
extensions on the official website.

![](/images/2022-05-21-15-00-04.png)

You should really give Gitmojis a try. It can only improve your productivity.

---
### Conclusion

Gitmoji really makes sense when working with others. It helps you and your
collaborators working faster. Adding emojis to your commit messages will make
your repositories beautiful and colorful. I am sure it will make you an even
happier person.

> If you are using Gitmojis in your project, share the word by adding this badge
at the top of your project!
> {{< rawhtml >}}
<a href="https://gitmoji.dev">
  <img src="https://img.shields.io/badge/gitmoji-%20😜%20😍-FFDD67.svg?style=flat-square" alt="Gitmoji">
</a>
{{< /rawhtml >}}
