# Git

## Branch Structure

The ctedu-dev git repositories all follow the same pattern. Follow this documentation to maintain a consistent code base.

### Main branch

All of the branches in our projects are based off `main` by default.

### Branching off of main

When you want to create a new branch, you need to base it off of `main`, follow the steps below.

First, make sure your current branch is main, and then you can create a new branch and check it out.

```
git branch
```

```
git branch new-branch
```

```
git checkout new-branch
```

<!-- ![Branch Off Main 1](/img/branch-off-main-1.png) -->

<!-- ![Branch Off Main 2](/img/branch-off-main-2.png) -->

### Pre-Live

By default, whenever you create a new **pull request** in the github dashboard, our custom actions will automatically generate a pre-live link for that branch upon a successful build.

:::note
Typically we use the pull request button in github. If you'd like, you can figure out the config for this pull request command via CLI and share it here :smile:
:::

Check out this example below:

![Git Pre-Live](/img/github-pre-live-2.png)

You can find the pre-live link for the main branch in the Firebase dashboard. Under the Hosting tab, select your project and scroll down to Preview Channels.

![Firebase Pre-Live](/img/firebase-pre-live.png)

### Going live

When you want to push your code live you have to follow a few simple steps.

If you are working on code that branched off the main branch, you first need to merge your changes into main.

```
git checkout main
```

```
git merge your-branch
```

Make sure to commit and push your changes.

```
git add .
```

```
git commit -m '.'
```

```
git push
```

Now, you will rebase `main` onto `live` to maintain a clean history of commits.

```
git checkout live
```

```
git rebase main
```

```
git push
```

Always follow these steps to avoid a divergent commit history and to ensure consistency with your fellow developers. :sunglasses:


## Actions

Documentation coming soon