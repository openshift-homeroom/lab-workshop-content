If you need to run a workshop for many users, instead of the `deploy-personal.sh` script under the `.workshop/scripts` directory, you can use the `deploy-spawner.sh` script.

This script supports a number of different modes for spawning multiple instances of a workshop. These are:

* `learning-portal` - Used for workshops, or a permanent interactive learning portal where users are anonymous and may do a workshop at any time. Users are given temporary access as a service account user, with a single temporary project. When a workshop is completed, or the allowed time expires, the service account and project are automatically deleted.

* `hosted-workshop` - Used to run a supervised workshop where each user is provided with separate login credentials for an existing user of the OpenShift cluster in which the workshop is being run, in order to login. Users can perform any action in the cluster that the OpenShift user can do, including being able to create multiple projects, if the cluster user quota configuration permits it.

* `terminal-server` - Similar to the hosted workshop configuration. It defaults to only supplying an interactive terminal in the browser using the workshop terminal base image. If a workshop using the full workshop dashboard base is used with this configuration, no embedded web console is provided.

* `user-workspace` - Similar to the learning portal configuration, but users need to login through Keycloak. Users are given access as a service account user, with a single project. The service account and project are dedicated to the user and will still be present if the user were to leave and come back at a future time. This provides a place where users can do ongoing work, but without needing to allocate users in OpenShift itself.

* `jumpbox-server` - Users login through Keycloak. It defaults to only supplying an interactive terminal in the browser using the workshop terminal base image. The user has no access to the cluster itself to do anything. The terminal would be used to access a separate system.

Except for `jumpbox-server`, multi user deployments using the workshop spawner require that you have cluster admin access.

When designing workshop content, you should keep in mind how you will deploy it. This is because the environment provided for a personal instance of a workshop, and the various ways of deploying it for multiple users, can differ.

By default when you use `deploy-spawner.sh`, it will use the `learning-portal` configuration for the workshop spawner. If you work out that a workshop requires a different mode when being run for multiple users, you can set the `SPAWNER_MODE` setting in the `.workshop/settings.sh` file.

If you want to work on your workshop content when using the workshop spawner, you still can. Run `build-workshop.sh` as you did previously. This time the workshop instance wouldn't be automatically restarted though. To do that, and have the new version of the workshop image used, select "Restart Workshop" from the menu of the dashboard for your workshop session run from the spawner.
