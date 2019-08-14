When you deployed the sample workshop you created during this workshop, you used the `deploy-personal.sh` script. This can be used with your own workshop image where a user is only interested in deploying the workshop image for their own use.

When this was done, the option `--settings=workspace` was used. This was required because of how this workshop has been deployed. It isn't something you would normally need, and instead, you would usually use only:

```
.workshop/scripts/deploy-personal.sh
```

The purpose of the `--settings` option is to allow additional custom settings to be supplied beyond the default settings for a specific workshop. This would be used where you need to override settings when deploying the workshop for a specific use case.

In this case, access to the workshop environment would normally be gated using user authentication provided by the OpenShift cluster, with only a project admin of the project having access to the workshop. In deploying the sample workshop as part of the workshop, we couldn't use that way of handling authentication.

Instead of relying on user authentication provided by the OpenShift cluster, you can though provide the `AUTH_USERNAME` the `AUTH_PASSWORD` settings, to enable access using HTTP authentication. What was therefore done, was that the file `.workshop/workspace-settings.sh` was included with the sample workshop content:

```execute
cat .workshop/workspace-settings.sh
```

The `--settings=workspace` option was used to specify that this additional settings file should be read. This was read after the `.workshop/settings.sh` file was read.

This enabled the specific workshop deployment to be customised as necessary. It was used here to change how authentication was handled when deploying a personal workshop when working on the workshop content. You could use it to refer to a different settings file for different versions of the workshop, using a different workshop image, or by specifying a different workshop file to enable different modules.
