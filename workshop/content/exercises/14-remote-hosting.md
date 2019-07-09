The recommended approach to distribute a workshop is to create a container image which packages up your workshop. By having everything packaged up as an image, rather than content needing to be downloaded when the workshop is run, it allows for a workshop to be run in disconnected environments.

If you don't have a requirement for running workshops in a disconnected environment, and instead want to use a hosted Git repository as the source of the workshop content, you can, but you will loose the ability to bundle additional applications or source code files.

To deploy a workshop from a Git repository, you can use:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param DOWNLOAD_URL=https://raw.githubusercontent.com/openshift-homeroom/lab-markdown-sample/master/workshop \
  --param WORKSHOP_FILE=workshop.yaml \
  --param APPLICATION_NAME=lab-markdown-sample
```

The `DOWNLOAD_URL` template parameter should define the URL for where the workshop is hosted. This needs to correspond to the `workshop` directory, not the root of the Git repository.

The `WORKSHOP_FILE` template parameter can be optionally supplied if you need to select a workshop file other than the default of `workshop.yaml`.

The templates provided for `workshop-spawner` also accept these template parameters.
