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

## .gitignore file
When working with Xcode projects GitHub has a nice template for it. Xcode generates a lot of files you don't need in your source code repository (like DerivedData or dSYM files). You normally don't commit the source code of Pod files or from SPM.

## .githooks
TODO

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
You can setup templates for your Pull Request, this helps tremendously becaue every Pull Request looks the same and nothing is forgotten. This can include link to your Jira Ticket, Screenshots, How to Test and so on.

### Pull Request: Code Review vs Testing
#### Code Review
When doing reviews there are two things that you can do. First you can do a code review by reading the code and maybe spotting some mistakes there. This can be done rather quick (depending on the size of the PR) and often in the 'dead area' before a meeting. If I just do code review and no testing I state that in my review.

#### Testing the PR
The other thing is to checkout the branch and really test out the new feature from an end user perspective and you may you stumble upon an edge case. This kind of review takes much more time but is very valuable. You learn more about the feature that has been developed.

Checking out a branch and running some setup scripts (like `pod install`) can take some time, I often need to close Xcode, then Xcode is indexing, may you need to clean the build folder and so on. I just recently learned option is to checkout the repositry twice at different locations, so that you don't f#ck up your current working directory.

As those tasks (setup, cleaning, building, running) can take some time it is often a good task to do after a meeting when your brain is tired and you click around like robot and wait.

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

### Draft PRs
Make it clear for your team members that your PR is not finished yet! I like to use the `Draft PR` feature of GitHub for that. It is a quick way to show my team members that I am working on this task, but I don't have to write a detailed description yet. You could also use a `wip` (Work In Progress) label, or put **WIP** in the title of the PR.

### Reviewing again
If you have the principle of 2 other people reviewing your PR it can be cumbersome to ask them to review your PR again after you made their proposed changes. However is also possbile to keep the approved status from them, which is a real blessing!

## GitHub Actions
TODO: For every PR, Nightly, Release,... Translations, Dependencies
May use different machines for different tasks is possbible: Linux is cheaper than Mac

## Review Process: Tests and Linters
TODO:

## Review Process: Danger
[Danger](https://danger.systems/swift/) can be used to analyze your Pull Request and warn you when Pull Request size is rather large. It is also a good reminder to try to keep your commits as small as possible. Danger has other cool features so checkout their documentation.

## Cloning a repository: SSH
While it works cloning a repository with user-name and pasword it would get pretty annoying to log in every time if you would push from the command line. It is also annoying when you had to change your password connected to your companies Identy Provider. Getting those `ssh` keys for cloning a repository is not obvious to everybody, so don't be afraid to ask. I remember saving my `ssh key` at a secure place and putting it back into the correct directory and `chmod` the `ssh key` after I got to setup a new Mac.

## git-crypt
Storing credentials is hard. Everybody needs them to use certain internal APIs. One way to check in certain credentials into git is via `git-crypt`. The `git-crypt` key file can be shared withing your team via 1Password for example.

On the other hand files like a `Google-ServiceInfo.plist` are not that critical, so you are fine without encrypting them.

## Merge conflicts with projects files 😭
When working with an Xcode project with multiple people you will experience merge conflicts with the `.xcodeproj` file... Fixing those conflicts is really awful. One way to solve this is via [tuist](https://tuist.io). With tuist the `.xcodeproj` is not checked into git, you create your project locally with tuist. Goodbye merge conflicts! Another tool would be `xcodegen`.

## Merge conflicts / changes Storyboard files
Storyboards are a NIGHTMARE to solve merge conflicts, I would advice to sync in your team WHO touches WHICH Storyboard. Also modularizing storyboard can help tremendously.

# Additional topics
* SwiftGen (Assets, translations)
* How to handle developer certificates (fastlane)
* Handeling TODOs
* Dependency Injection
* Differnt bundles for dev and prod
* Translation process - Phrase.com
* Accounts for Firebase
* Remote Config (Firebase) / Feature flags
* Dealing with Xcode warnings
* Bumping the build number
* Debug menu inside the app - different environments (dev, qa, prod)
* Network Debugger
* Sharing Passwords (1Password)
* Onboarding Guide: get a Google Account, join Apple Developer team, ...
* Analytics / Tracking
* Architecture Diagrams and Desicions
* Who takes care of the developer account?
