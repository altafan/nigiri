# Contributing

The modus operandi for opening PRs is a bit tricky due to how go manages the import paths.

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

We use drone v0.8, refer to [this](https://0-8-0.docs.drone.io/cli-installation/) installation guide.  
You don't need to follow any other further configuration step if you just want to run `drone exec`.
