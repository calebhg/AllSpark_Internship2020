# Git & Versioning

Git is a version control system created by Linus Torvalds that tracks changes to files and allows multiple developers to work on a project at a time.

## Basics of Git

### Cloning

At the start of a developer's work on a project, the developer does what is called *cloning* the project. This gives them a copy of the project on their machine that they can independently modify. This is the basis of how `git` works: many developers each `clone` the project onto their machine, and the project is maintained by each of their modifications to the project.

Cloning a project can be done through the command line via the command:
```
git clone <url>
```

### Branches

A branch is a set of revisions to a project to add a feature, and as well is often used to contain fixes for a set of bugs. This allows a developer to work on multiple features or bugs at a time without them conflicting with each-other. Another useful feature for branches, is a project can selectively pick-and-choose features & bugfixes. This is important because features may be very large or small, and a project can continue to release new features or fixes while others are still being developed. We will see more of this in the versioning section.

##### Feature Branches

There are a set of common branches often seen in common-practicing projects:

* `master` contains the current project under active development
* `stable` contains the project in its most recent stable state (it doesn't crash or throw errors)
* `nightly` contains the project with its most recent feature, similar to `stable`, but is not considered in a stable state (users beware)
* `<tag>` (for example `1.0.0`) contain all the features included in that `tag` (more on this later)

You may also see another very similar branching strategy. Under this methodology, developers work off of a `development` branch. When `development` is tested, it is moved to `master`. When a new release is to happen, `stable` is moved into `release`. This methodology is much more common in web development, the former being much more common in libraries. In this methodology:

* `release` contains the project that the users will see
* `master` contains the project in its most recent stable state
* `development` contains the entire working project
* `<tag>` refers to the version of the project

Branches are often described as *short-lived*. This is to mean that a branch only contains a singular feature or bug fix, and the branch is to be abandoned or deleted when this is accomplished.

A branch can be checked out through the command line through the command:
```
git checkout <branch_name>
```

A branch can be created **from the currently checked out branch** through the command line with the command:
```
git checkout -b <branch_name>
```

#### Staging & The Stash

Internally, `git` keeps a stack containing all the changes created per branch. This allows a developer to pick and choose files to include in a branch. This is often used in a situation where one file is modified only to allow easy reproduction of the feature, while the feature is contained in a different file. A dev may stage the file needed without redoing the work on all the files.

Most commonly developers will add all files as they need to be staged to commit, and rarely do extra files need to be ignored.

Files may be added to staging via the command line with:
```
git add <file_or_directory>
```

#### Committing

When files are done in staging and changes are finalized, the changes are added to the branch by committing the changes. Typically a developer will commit many times in a branch. Similar to other `git` behaviors, this allows a developer to selectively pick and choose changes on a branch. This practice is known as ***cherry picking***. A commit comes with a message, that describes the changes done.

A commit may be done to a branch via the command line with:
```
git commit
```

#### Pushes and Pulls

A pull request in the shortest terms is a request for a branch to include another branches changes.

For example: `feature/branch_a` can request `feature/branch_b` to include `feature/branch_a`'s changes.

Opposite of a pull, is a push. This behavior as expected, is the opposite of a pull, where a developer may push the changes to a branch.

Frequently, a branch is controlled with who can modify and change a branch. While pushing is simpler and easier, often a pull request is required.

#### Tagging

Tagging is an important tool that allows a project to keep "tags" to specific versions. Typically a project has a branch with the name of the tag permanently checked out to that tag. This allows people using the project to keep using the project at that state without worrying about changes. In this example, another project may be using a specific feature or relying on a certain interaction from a specific version of a project, staying at a specific tag means these interactions will never change, while the project relied on may continue to change.

# Versioning

Versioning is a practice done to keep track of specific changes to a project as specific versions or modifications, denoted by a version number (e.g. `1.0.0`). This numbering is done many ways, but the most common and most accepted method is denoting it as major.minor.patch. When a `major`, `minor`, or `patch` is done, the corresponding number is incremented by 1, and all numbers following are reset to 0.

#### Patch

The smallest revision that may be done is a `patch`. A patch contains simply a bug fix or set of bug fixes. These do not contain any changes to the project other than these bug fixes.

Typically, when a project dependency is created, the patch number is ignored.

#### Minor

Minor contains smaller changes to a project without adding entirely new features or changes. These are most typically optimizations to a project that have no serious changes.

Typically when a project dependency is created, the minor number is specified, as it is considered volatile.

#### Major

Major contains new features or entire reworks of a project. Typically these are only new feature introductions, as the projects inner-workings are already considered finalized at this point.

Typically when a project dependency is created, the minor number is specified, as it is considered volatile.

#### Exceptions to the rules

Typically, we see don't see the Major number at `0` in a project's version. Typically, `1.0.0` is a marker that marks when a project becomes completely stable and more importantly ***is considered finalized in its behavior***. Before a project hits its `1.0.0` marker, the project is subject to a lot of change; the developers may find the way a library works just doesn't fit, they may not even like it and make whole new changes to it. Because of this, typically projects do not create dependencies on anything marked with a Major version of `0`.

This practice can become very confusing in newer languages, when libraries are marked Major version `0`, despite being stable and feature-complete. It should be noted that this happens because the language is not considered stable or feature-complete. In these instances, you may see projects last years marked as `0.x.x`, despite being stable and feature-complete for a very long time.

Special Versions:

* `1.0.0`, as previously mentioned, is when a project/library first becomes stable and feature-complete

* `0.1.0`, typically a proof of concept or when it first becomes working but is not considered feature-complete or stable
