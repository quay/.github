# .github

## Workflow Templates

### Build and Publish

Builds and publishes container images to the configured repository.

#### Configuration

The workflow's predefined configuration will suit most of the repositories in the Quay organization.
Continue reading if your repository doesn't follow the same conventions.
Note that configuring a workflow is done once you select the workflow in the destination repository.

##### `.on.push.branches`

The workflow is triggered by pushes to branches matching the `redhat-**` expression. This will match
all Y-stream branches. If your repository doesn't track versions in such a manner, go ahead and
updated your workflow triggers.

**IMPORTANT** make sure to update the `BRANCH_PREFIX` job env accordingly.

##### `jobs.build-and-publish.env.BRANCH_PREFIX`

The branch prefix (example `redhat-`) is used to get a version number from the branch name.
For example, a branch named `redhat-1.5` will yield a version number `1.5`.

**IMPORTANT** this value must match the one specified on `.on.push.branches`, save for the `**`.
For example, if `.on.push.branches` is `release/**`, then `BRANCH_PREFIX` should be `release/`.

##### `jobs.build-and-publish.env.REGISTRY`

The registry where the final container image will be pushed to. For example: `quay.io/quayproject`.

##### `jobs.build-and-publish.env.REPO_NAME`

The repository name on the registry.

Defaults to the github repository name.

##### `jobs.build-and-publish.env.TAG_SUFFIX`

Suffix to be added at the end of the container image tag.
If the tag is `1.2.3` and the suffix is `-nightly`, the end result will be `1.2.3-nightly`
