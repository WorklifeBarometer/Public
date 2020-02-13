Code review
------------

We, as developers, generally dislike needless bureaucracy, such as meetings, documentation, etc., which isn't fun and makes us in-efficient and bored.

Therefore, each disturbance that is placed on developers is weighed rigorously for its pro's and con's.

Code review is one of those processes that we've considered to be worth the effort.

We review essentially every line of code that is written via bi-weekly video skype meetings. Here are the pro's and con's:

Pro's:
- Increase quality of the code, both from getting criticism and comments as well as from having to simply explain one's code
 - Fewer bugs
 - Better architecture
 - Fewer security issues
 - Fewer duplicates of previous code
 - Etc.
- Knowledge sharing between developers
- Increased motivation for writing code, especially high quality code that can impress one's co-developers
- Discover blockages and bottle-necks earlier (although not as early as with daily stand-ups)

Con's:
- With all developers assembled at once it is a major drain on time, especially for part-timers who spend proportionally more time on this. However: Part-timers have a higher need of the benefits, since they aren't as big a part of the day-to-day office routine.
- They can be boring to sit through
- Both of the above can be alleviated by following the below advice on how to use git


Git process
--------------

Git is a powerful revision control system. However, it isn't obvious how to get the most out of it. To facility both the code review process described above and to achieve a nice log history we abide by the following rules:

- Use small commits. This is measured on a mental load metric. If you are changing spacing or line endings in 100 files, do it in a single commit. If you are implementing a class and another class that calls the first one, probably do it in two commits.
- Don't pull. Fetch and rebase instead. Pull will create a nasty history that's hard to review and it will mess up your history.
- Commit often. Push often. Fetch/rebase often. Thanks to interactive rebasing you'll end up with a nicer history. And you avoid losing code.
- Use interactive rebasing to hide your mistakes. While they are fun to talk about, and you should, at code review, mistakes are boring to review. So use the squash, fixup and reword actions in interactive rebase to polish your pull request before you push.
- Use short-lived feature branches. Long-lived branches are tedious to keep up to date with the main branch and also tedious to review.
- Don't use "git push" or git pull. Instead, use "git fetch" and "git push origin branch-name".
- Don't keep a local master branch. Only write to master through pull requests. With a local master you risk overwriting the remote master.
- Write descriptive commit messages. In the first line, which should be short, write what you did. Keep the second line empty. In the third line, write why you did what you did, if it isn't obvious. And keep in mind the reader might not be familiar with the method/system/language you are writing, so it might not be so obvious to you.
- Try to have every commit build. Eg. first write the system-under-test, then the test. This will be nice for git bisect and also for review.
- Set up keychain management so you don't have to write your password all the time. Which would make you slack on the above.
- Set up git branch completion, so you don't have to type long branch names. Which would make you choose lazy short branch names.
- Don't use a git client that goes against the above rules. Git gui is a nice client. So is the command line.

Example usage:

```git
git fetch
git checkout origin/master
git checkout -b my-new-feature-branch
git commit -am "My awesome change"
git fetch
git rebase origin/master
git rebase -i origin/master
[... use squash, fixup, reword ...]
git push origin my-new-feature-branch
```

Task flow
--------------

We use a light-weight [kan-ban](https://en.wikipedia.org/wiki/Kanban_(development)) approach as opposed to SCRUM (~80 rules) or even heavier methodologies such as PRINCE2 (1000+ rules). In addition we've stolen a couple of the SCRUM rules as we've seen fit as well, but we don't run SCRUM in any kind of religious manner.

So, what are the three kan-ban rules?

1. Visualize your workflow
2. Limit work in progress (WIP)
3. Pull rather than push

In addition, we create work breakdown structures and do estimates using planning poker. We do not however, estimate in points, we estimate in hours, which is a big no-no in SCRUM. We only do this for projects that take longer than a day to complete. We also skip it if the nature of the work is highly experimental or exploratory in nature.
