The recommended approach to distributing a workshop is to create a container image which packages up your workshop. By having everything packaged up as an image, rather than content needing to be downloaded when the workshop is run, it potentially allows for a workshop to be run in disconnected environments.

If you don't have a requirement for running workshops in a disconnected environment, and instead want to use a hosted Git repository as the source of the workshop content, you can, but you will loose the ability to bundle additional applications or source code files.

To deploy a workshop from a Git repository, edit the `.workshop/settings.sh` file and remove the entry for `WORKSHOP_IMAGE`. Doing this will mean that the default dashboard base image will be used. At the same time, add a setting for `DOWNLOAD_URL`.

The `DOWNLOAD_URL` setting should define the HTTP server URL for where the workshop content is hosted. This needs to correspond to the `workshop` directory, not the root of the Git repository.

If you were using GitHub to host the workshop content, you would use the GitHub URL for raw content. For example:

```
DOWNLOAD_URL=https://raw.githubusercontent.com/openshift-homeroom/lab-markdown-sample/master/workshop
```

When the settings are defined this way, the workshop will be deployed using the default dashboard base image, but when the container starts up, it will download the workshop content from the HTTP server. Which files to download for the workshop content will be determined from the workshop and modules file.

When this mode is used, you cannot have `build` or `setup` scripts, nor have slides. Any files outside of the workshop directory will also not be available for use during the workshop.

You can add a `WORKSHOP_FILE` setting in `.workshop/settings.sh` if you need to override which workshop file is used.

If you need additional command line tools or packages available, you can create a custom dashboard image with those, but without any workshop content added, and refer to that image on an image registry using the `WORKSHOP_IMAGE` setting. It will be used in place of the default dashboard image.
