When done with a workshop and you want to delete everything, if it is a personal workshop deployment, you can run:

```execute
.workshop/scripts/delete-personal.sh
```

Do this now and it will clean up your deployment of the sample workshop content.

Because you built the workshop image from local files in the Git repository, you should also run:

```execute
.workshop/scripts/delete-workshop.sh
```

This will delete the build configuration and image streams for the workshop.

If you used the workshop spawner, you would instead run:

```
.workshop/scripts/delete-spawner.sh
```

and if you built the workshop from local files when using the workshop spawner, once again run:

```
.workshop/scripts/delete-workshop.sh
```

In the case of using the workshop spawner, if the workshop had been setup to deploy special global resources in the cluster, you may also need to run:

```
.workshop/scripts/delete-resources.sh
```

You should refer to the description of a specific workshop to determine if that is necessary, or when you should run it.
