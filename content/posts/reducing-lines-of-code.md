---
title: "Reducing Lines of Code"
date: 2019-05-14T14:55:29-07:00
draft: true
toc: false
images:
tags:
  - Development
---

One thing that I've noticed as I review pull requests is that there is a tendancy to open pull requests were the diffs are large. Looking at a pull request where hundreds of lines of code changed can be intimidating. I am a fan of succinct and concise pull requests. I want to outline a couple common pitfalls that I've seen developers fall into when opening pull requests for review by peers.

# Pitfall #1: Mega Reviews with many changes

Reviewing a commit that says something like

```
Add new feature X

Also fixed the broken thing
Deleted unused code
Refactor large module into smaller pieces
Added additional docstrings
etc...
```

Rather than creating a mega review that lumps together multiple changes, I am prefer more frequent, smaller reviews. I think developing a culture where a team reviews pull requests quickly, especially if they are smaller, is healthy. It makes it easier to detect bad commits too as your CI pipeline will deploy smaller changes more frequently. **Don't discourage small reviews or reviews with only couple lines changed — those should be easier to review quickly anyway.**

# Pitfall #2: Reimplementing what a library can accomplish

I am a big fan of abstractions and using libraries where possible. If there is code/logic that is reusable, I am a strong believer that it should be encapsulated in a library or module. I am also a fan of building modules on top of existing modules to provide higher-level functionality. For example, I really like Python's [`subprocess` module][1], as it provides a higher level `subprocess.run` method but also exposes lower-level methods like `subprocess.Popen` for the nitty-gritty when you need it. Most use cases should use `subprocess.run` unless you specifically need a reason to use one of the underlying methods. 

So when I see pull request where the submitter used `subprocess.Popen` and a bunch of additional code to do the stuff you get by using `subprocess.run` for free, I see it as an opportunity to reduce the lines of code. **Use higher-level functions where possible and leave it up to the library maintainers to hide the implementation details from your code.**

# Less is more

At the end of the day, every line of code is a liability. Every line of code is going to require maintenance, it's going to require reading and re-reading by different developers. It is in our best interest to write as little as possible to accomplish what we need to do. By writing [DRY][2] code, we can further reduce the chances of making the same mistake in multiple places as well. 

[1]: https://docs.python.org/3/library/subprocess.html
[2]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself