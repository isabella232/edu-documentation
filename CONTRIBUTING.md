Contribution Guidelines
=======================

This document describes the general guidelines for contributing to Puppet
Education project repositories. This includes aspects of the git workflow,
commit message conventions, and reviewing standards that are general to all of
the team's repositories. Where a repository requires guidelines in addition to
these general ones, those guidelines are documented in the project's own
CONTRIBUTING.md document.

## External Contributions

External contributors making significant contributions to our projects must sign the
[Contributor License Agreement](https://cla.puppet.com).

For [trivial changes](https://puppet.com/community/trivial-patch-exemption-policy),
no signature is required.

## Workflow

### Initial setup

Anyone who wants to contribute needs a [GitHub account](https://github.com/signup/free)

Puppet employees need a [Jira account](https://tickets.puppetlabs.com) to create
and track tickets.

Create a new fork of the repository within your own GitHub user namespace.

Clone the fork to the computer where you will be working.

    git clone https://github.com/puppetlabs/<repo>.git

Add the original puppetlabs/<repo> as a new remote called "upstream".

    git remote add upstream https://github.com/puppetlabs/<repo>.git

### Jira tickets

Most changes to Puppet Education repositories should be tracked by a
corresponding ticket in Jira. With the exception of certain minor changes ([see
below](#making-commits)), Puppet employees working on Puppet Education project
repositories must create a new ticket or base their work on an existing Jira
ticket. In the case of outside contributors, we do not require a ticket to be
created or referenced prior to submitting a pull request. In this case, the
reviewing member of the Education team will handle any status changes to
existing tickets as part of the review process.

The steps to begin work on a new or existing Jira ticket are as follows:

* If no ticket exists, create one. Clearly describe the issue. If it is a bug,
include the steps to reproduce it.
* Assign the ticket to yourself.
* Change the status of the ticket to "In Progress".

### Setting up a feature branch

From your local clone of the repository, check out the master branch, pull any
new changes from upstream, then create a new feature branch. Any branch naming
system that helps you track your local branches is acceptable. If there is a
related ticket in Jira, you may prefix the branch name with the ticket ID.

    git checkout master
    git pull upstream master
    git checkout -b COURSES-979-fix-dns

### Making commits

Work in your local repository to make the changes needed to address the
issue you're working on. Commits should be atomic and only introduce changes
related to the issue you are working on.

Do not include changes to version numbers or change logs in your work. Rather,
include a sufficiently descriptive commit message to facilitate collating
changelog entries that will be added in the next release.

In most cases, the commit title should follow the `(TICKET-NUMBER) SHORT
EXPLANATION` pattern. The title is limited to 75 characters, so be concise.

    (COURSES-9590) Add host resources to list of topics

If there is no ticket, use the (DOC) prefix for documentation changes or the
(MAINT) prefix for other changes, for example:

    (DOC) Add comments to resource declaration

or

    (MAINT) Fix whitespace

Include comment below the title and separated by one empty line. The comment
includes a more verbose description of the change. The comment should adhere to
the following guidelines:

- When working on a ticket, use the following pattern on the first line of
your commit comment to trigger the Jira integration `COURSES-9790 #resolved #time 10m`
- Write *why* you did what you did first
- Write what changed
- Write how it affects others (projects, people, processes)
- Add a brief description of what you did. This is more important for large
  PRs, where the reviewer could use help in understand what you did.
- Add a note mentioning what you tested and how.

The following is an example of a well formed commit message, including a
concise title and full comment:
```
    (TRAINTECH-1133) Create general contribution guide

    Currently, contribution guidelines for Puppet Education repositories are
    maintained separately in their respective repositories. This can lead to
    divergent practices and/or a higher maintenance burden.
    
    Add general contribution guidelines that apply to all Education
    project git repositories. These exist in a new edu-documentation
    repository so they can be referenced from the specific contribution
    guidelines in each separate project repository.

    Before the associated TRAINTECH-1133 ticket is marked as resolved,
    other repositories must be updated to link to these new guidelines and
    remove redundancies.
```

It may take several iterations of commits and testing before you arrive at a
final set of changes for a PR. When you are ready to submit a PR, squash
intermediate-work into a final, well-formed commit. This makes a project's
commit history more legible. See this
[documentation](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History) for
specific information on amending and squashing commits.

### Testing

Before making a pull request, ensure that you have made any necessary changes
to the repository's test suite and that the (updated) tests are passing.

Generally, you should consider the following steps to validate your work before
creating a pull request:

* `puppet parser validate`
* spellcheck
* Use puppet-lint
* Check for unnecessary whitespace with `git diff --check`
* Run any existing spec tests

Review the specific documentation in the repository you're working on for more
guidelines on testing. Some repositories require more complex testing involving
new VM builds and a full suite of acceptance tests before a pull request can be
merged.

### Pull request

Create a PR from your fork to the upstream fork. If you followed the commit
message guidelines above, you will not need to add anything to the description.

    git push upstream <branch> 

Navigate to the upstream project's GitHub page in your web browser and use the
GitHub interface to create a new pull request.

### Reviewing work

When reviewing a pull request, please:

* Help others stick to the practices above, by reminding them gently.
* Do not merge PRs until they meet the standards described above.
* When in doubt, offer to help someone improve their PR.
* Add comments in-line by clicking on the line number in the file (and not as a general comment
   on the PR page with a named reference to a file or line).
* Ensure that tests have been run and are passing. If you are not familiar
with the testing and release workflows associated with a project, do not merge
a pull request in that project until you fully understand how it has been
tested.

### Making a release

Where a project has an associated version number, we follow
[semantic versioning](http://semver.org).

Please see specific guidelines in each repository for documentation on the
release process.
