# github-release-example
An example of how an approval for release to a protected environment in GitHub can be
logged as an attestation in Kosli.

## How to demo

### Build a new version of backend
Make a branch for your change
```shell
git checkout -b backent-next-version
```

Simulate that you have done a change to the backend by increasing the `counter` in
```shell
apps/backend/backend-content.txt
```
Commit and push the change to GitHub.
Create a Pullrequest and merge the change back to main.

This will trigger a workflow in [GitHub](https://github.com/kosli-dev/github-release-example/actions/workflows/build-deploy-backend.yml)

You now have to approve the deployment to `staging envirnment`

You should now have a trail that matches the commit in the 
[github-release-example-backend](https://app.kosli.com/kosli-public/flows/github-release-example-backend/trails/) flow.
The trail should have an `artifact` and a `pull-request` attestation.


### Release of SW to production
We now want to release the new version of the backend.

Add and push a new version tag.
```shell
tag=v0.0.16
git tag -a $tag -m "Version $tag"
git push origin $tag
```

This will trigger the same workflow in [GitHub](https://github.com/kosli-dev/github-release-example/actions/workflows/build-deploy-backend.yml)

The trail name will match the version tag.

Approve the SW for staging first, and then for production.

In the Kosli trail for the release you will now have a `release-approval` in addition to the pull-request and artifact.
