# Skyedocs

## Setting up your environment

To get your mkdocs environment configured; install the following:
* python (min 2.7.13):
* mkdocs:

        pip install mkdocs

Note: you might need to ensure cinst, python, & pip are all in your path.

## Updating the documentation

The **Skye**docs repository has all the documentation in markdown format. There is also a submodule to the **skye**.github.io GiHub pages repository, which is basically the **skye**docs repository transformed into static HTML for the web.

To update the documentation the following steps need to be done.

* clone the repository and cd into it

* There are 2 branches:

| branch name       |    description     |
|-------------------|--------------------|
| **master**        |    master branch for **skye** docs (https://docs.skyecared.com.au) |
| develop           |    dev branch for **skye** docs |


## How to contribute

* You can create a branch for your changes.

        git checkout -b new-thing

* Make your changes to the documentation.
* Run the web-application locally:  

        mkdocs serve --config-file mkdocs.yml


* Commit your changes and push your branch back up to GitHub.
* Submit a PR.
* When the PR is merged into the "master" branch, the Appveyor build will automatically push the generated content up to the associated AWS S3 bucket.

