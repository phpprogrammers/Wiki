How to use Git and GitHub
======

If you are new to GitHub it's might look like a mess in the beginning. But that's only until you've started to get the hang of it.

This document will show you some of the main things to know.

Fork a Repository
======

If you want to contribute, or use a project that lives on GitHub there is two things you will have to do.

For a detailed explination read [Fork A Repo](https://help.github.com/articles/fork-a-repo)

1. Fork the repository

Go to the repository you want to fork and click "Fork". GitHub will now make a repository on your profile with the same name as the one you forked

2. Clone it to your computer

To be able to do this you will have to install Git on your computer. Here you will find downloads for Linux, Windows, Mac OS X and Solaris. http://git-scm.com/downloads

Next, browse to the directory you want to clone the repo to. Open the Git bash and enter the following

```
git clone https://github.com/[yourusername]/[repository].git [foldername]
```

Keep in mind that when you clone it will create a new folder. If you do not enter a foldername, the folder will get the same name as the repository.

Push and Pull Request
======

Ok, so now we have cloned a repository and we want to contribute to it. What to do from here?

Let's say you have now done some changes. You now will have to add, commit and push and that is done by the following commands

1. Add new files, changes and deleted files.
```
git add -A
```

2. Commit the changes
```
git commit -m "Commit message"
```

3. Push the changes to your repository
```
git push origin master
```

Ok so that's it right? No. There is one more thing you will have to do. So far you have only updated your personal fork of the main repository. What you need to do now is to send a pull request to the repository you forked, which really is a simple process.

Open up your fork and click the "Pull Request" button. Fill out the form properly explaining what you have done, and click "Send pull request".

You can also see all the commits and changed files. This gives you the opportunity to do a last check before you send the pull request.

Keep your fork up to date
======

So far we have forked and cloned a repository, made changes and pushed them back and sent a pull request. But what now? What if someone does any changes to the main repository? Will you get them automatically? Nope. We need to add an upstream.
 
 ```
 git add remote upstream https://github.com/[username]/[repository].git
 ```

It's important that the upstream remote points at the main repository, the one that you forked. Not your personal fork of the project

So when you have added the upstream this is how you update your fork

```
git fetch upstream
```

Update your local copy
======

So now you have fetched changes from the upstream, you need to update your local copy as well. Just enter the following, and you're done.

```
git pull origin master
```