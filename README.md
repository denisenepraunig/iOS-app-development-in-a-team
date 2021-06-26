# iOS-app-development-in-a-team
Things to consider when developing iOS applications in a team. These are the things I learned while working on iOS projects with multiple team members.

# Version Control: git and GitHub

## Git and GitHub
The current standard I seems to be `git` and GitHub is a convenient way to host your source code. There enterprise options available so that you could sign-in with your companies Identity Provider. One great benefit of GitHub are their GitHub actions which can be used to automate tasks, like building and testing apps. 

## Hosted vs public cloud GitHub
There are public and self-hosted options available. Self-hosted options require a VPN connection to your companies servers which can be cumbersome sometimes. I haven't experienced any downsides of using the public available GitHub.

## GitHub organisation
If you are using GitHub as to host your source code your department may create a GitHub organisation to keep the various projects of your department together in one place.

## GitHub e-mail notifications
Which e-mail address should your developers use to join your GitHub organisation? Should they create accounts with their company e-mail address? Some may already have private GitHub accounts with their own private e-mail addresses. Is it allowed that developers receive GitHub notifications to their private email addresses? 

## GitHub adminsitration
Who takes care of inviting developers to the organisation, who adds them to the repositories they should work on?

## Protecting the main branch
Based on your teams working style it may be a good idea to protect the main branch - so no one can directly commit to it. However I've also worked on a rather small team without any review process were everything was directly commited to main and you justed fetched and merged.

## Repository README
TODO: Project setup, contribution guide

## Branching strategy
This can be a big topic to discuss. The style I've been working on the most time was a `main` branch which was the basis for a `release` branch later on. Everyone created their `feature` branch and after their Pull Request was reviewed it was merged into the `main` branch.

## Naming Branches
TODO: feature-jira-ticket or my-name/jira-ticket

## Rebase vs Merge: Branches
### Merge main into your branch:
In my previous team we had a `feature` branch and we kept it up to date by merging the `main` branch into it regularely. It works but the commit history looks super cluttered. Multiple people could work together and merge each others changes into their branches.

### Rebase your branch onto main:
In my current team only one person **owns** their branch, so they are allowed to do whatever they want with their branch. Rebasing IS changing the commit history, if you work together with another person on that branch you should communicate what you are doing. If you did rewrite the history in your branch THEN you need to do a `force push` to the remote branch. Don't be fooled by the term `NeVeR dO a FoRce PuSh` - I felt for this trap and was 'afraid'. However it is my branch, I know what I do - `rebasing`, `squashing`, ... However IF you work with another person please sync upfront to NOT overwrite their pushed changes 😅. Another note to force push: yes be EXTRA CAREFUL if you would EVER need to force push to main. Know what you are doing! 

With rebasing I tend to squash my commits together because if merge conflicts occur while rebasing onto main, then those things would be repeated for each commit. Rebasing has a really nice linear history which is easy and clear to read.

## Review Process
### Pull Requests in General
Code reviews are a good possiblity to get familiar with different parts of the applications. You need to decide how many people should approve your Pull Request, two people seems to be a good option. One person is often the person you paired during your task, the other person is another team member. Sometimes it can get quite stressful with needing two reviews, especially if a deadline is approaching and everybody is busy and you need your changes merged for some releases.

However you will experience some certain team dynamics, some people are SUPER nit-picky/religous about certain things (example: immutabilty at ALL costs), so you may try to quickly get other people to review your code before those discussions start 🙈. Some people are always like `LGTM`, some people are incredible at spotting unsued imports - so really try to balance WHO reviews your code.

### Pull Request: Template
TODO

### Pull Requests: Appreciate
When reviewing Pull Request we are trying to find errors or spot mistakes. If I receive a review with only highlighting your mistakes I feel a bit down, therefore I also try to point out some things like "Wow, that's a smart use case of a Set here" or "TIL (today-I-learned)" or put some 🎉 emoji into the review. Sometimes I comment my own Pull Request and say "@Team member thanks for this cool idea" (which came up during pairing or so).

### Review attitude
TODO
reviewing: let's make it better
getting review: OMG why can't it be perfect in the first place

TODO: image: 1000 lines LGTM, 10 lines ENDLESS discussions

### Pull Requests: Knowledge Sharing
One example is when I used a cool new Swift feature I put it into a **Knowledge Sharing** section of the Pull Request. 

### Review Process: Big Mob Reviews
In one team everybody committed to the `main` branch and regularely we had some big code review meetings with all the team members. We were sitting in a meeting room, the person who wrote certain files put connected their Mac to a beamer and all the team members could comment on the code. Changes were made directly during this review and commited. I also learned a lot from those kind of reviews as it as a great in-real-life discussion.

## GitHub Actions
TODO: For every PR, Nightly, Release,... Translations, Dependencies
May use different machines for different tasks is possbible: Linux is cheaper than Mac

## Review Process: Tests and Linters
TODO:

## Review Process: Danger
TODO: warns for big PRs...

## Cloning a repository: SSH
While it works cloning a repository with user-name and pasword it would get pretty annoying to log in every time if you would push from the command line. It is also annoying when you had to change your password connected to your companies Identy Provider. Getting those `ssh` keys for cloning a repository is not obvious to everybody, so don't be afraid to ask. I remember saving my `ssh key` at a secure place and putting it back into the correct directory and `chmod` the `ssh key` after I got to setup a new Mac.

## git-crypt
TODO

## Merge conflicts with projects files 😭
TODO: tuist or xcodegen

## Merge conflicts / changes Storyboard files
Storyboards are a NIGHTMARE to solve merge conflicts, I would advice to sync in your team WHO touches WHICH Storyboard. Also modularizing storyboard can help tremendously.

## git-crypt
TODO
Google plist files, not soooooo critical, but other files
