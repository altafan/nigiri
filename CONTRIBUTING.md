# Contributing

Hereafter is detailed how to proceed in order to contribute to Nigiri.

## Rules

The master branch is protected, thus it's in read-only mode. PRs are not directly merged into this branch, but we use a `staging` one to thorougly test the new changes before making them effective.  
Do not open PRs targeting the master branch because they will be **rejected**.

Pull requests must be shortly described into the comment and also must reference one or more open issues, in order to automatically close them when merging.

Pull requests must be the most granular as possible, i.e. they must close issues of the same category (eg. bug, new feature, enhancement...). Instead of mixing them into a single PR, open multiple PRs if it's possible, or explain into the comment that following PRs are needed.

Pull requests require one or more reviews from our team and must pass the CI build and tests to be merged.  
To facilitate the process of reviewing, force pushing is highly discouraged for 2 reasons: overwriting the commit history makes it unclear from a reviewer point of view; we use the squash and merge strategy, thus the (maybe long) commit history is merged as one single commit into master.

## Workflow

The modus operandi for opening PRs is a bit tricky due to how go manages the import paths.

At the moment, for the CI we use [Drone v0.8] and it's not needed any subsquent configuration step in order to test it locally with `drone exec`.

These are the steps followed by our team in order to correctly open a PR:

* Clone your fork in `$GOPATH/src/github.com/<your-github-user>/nigiri`
* Find and replace all `github.com/vulpemventures` import paths with `github.com/<your-github-user>` in the `cli/` directory
* Submit a commit with message `change import paths`
* Hack Nigiri
* Test your changes with `drone exec` to simulate locally the CI steps
* Open pull request

After we have reviewed the pull requests and CI tests and build pass, we'll request a last commit where you restore the import paths to `github.com/vulpemventures` with message `[CI SKIP] fix change import paths`.

**Note**:  
It's important to replace just the import paths of the go files in `cli/` directory. Other files use the same path for different purposes.
