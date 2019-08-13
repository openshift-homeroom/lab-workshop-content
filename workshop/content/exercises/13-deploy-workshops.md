This workshop was deployed using an OpenShift template included with the Git repository for the `workshop-dashboard` base image. This can be used with your own workshop image where a user is only interested in deploying the workshop image for their own use. The typical way of deploying a workshop for a single user using that template is to use:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/organization/lab-sample-workshop:X.Y" \
  --param APPLICATION_NAME=lab-sample-workshop
```

Access to the workshop environment will be gated using user authentication provided by the OpenShift cluster. Only a user who is an admin of the project the workshop was deployed to, will be able to access it.

Instead of relying on user authentication provided by the OpenShift cluster, you can provide the `AUTH_USERNAME` template parameter, as used with this workshop, to enable access using HTTP authentication. A generated password will be created which will be shown when the deployment is created, or you can query the deployment to retrieve it. Alternatively you can set a password using the `AUTH_PASSWORD` template parameter.

If you need to run a workshop for many users, a separate `workshop-spawner` application is available. This supports a number of different modes for spawning multiple instances of a workshop. These are:

* `learning-portal` - Used for workshops, or a permanent interactive learning portal where users are anonymous and may do a workshop at any time. Users are given temporary access as a service account user, with a single temporary project. When a workshop is completed, or the allowed time expires, the service account and project are automatically deleted.

* `hosted-workshop` - Used to run a supervised workshop where each user is provided with separate login credentials for an existing user of the OpenShift cluster in which the workshop is being run, in order to login. Users can perform any action in the cluster that the OpenShift user can do, including being able to create multiple projects, if the cluster user quota configuration permits it.

* `terminal-server` - Similar to the hosted workshop configuration. It defaults to only supplying an interactive terminal in the browser using the workshop terminal base image. If a workshop using the full workshop dashboard base is used with this configuration, no embedded web console is provided.

* `user-workspace` - Similar to the learning portal configuration, but users need to login through Keycloak. Users are given access as a service account user, with a single project. The service account and project are dedicated to the user and will still be present if the user were to leave and come back at a future time. This provides a place where users can do ongoing work, but without needing to allocate users in OpenShift itself.

* `jumpbox-server` - Users login through Keycloak. It defaults to only supplying an interactive terminal in the browser using the workshop terminal base image. The user has no access to the cluster itself to do anything. The terminal would be used to access a separate system.

Except for `jumpbox-server`, multi user deployments using `workshop-spawner` require that you have cluster admin access.
