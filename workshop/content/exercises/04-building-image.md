The recommended approach to distribute a workshop is to create a container image which packages up your workshop. This way, the workshop content, along with all the command line tools, runtime language environments and applications used to display the workshop content are together.

You can use `docker` or `buildah` to build the image using the supplied `Dockerfile`. If you have no need to install extra system packages, you could also use Source-to-Image (S2I) to build the image as the base image used in a `docker` type build, can also be used as an S2I builder.

In this workshop the ability to build the image using the `Dockerfile` will be used. Rather than use `docker` or `buildah`, we will setup a build configuration in OpenShift, pushing the workshop content using a binary input build. This will be done using the scripts provided with the workshop scripts package you added as a Git submodule.

To build our custom workshop image, we first need to deploy the sample workshop. To do this run:

```execute
.workshop/scripts/deploy-personal.sh --settings=develop
```

Note that the `--settings=develop` option is a special option being used in this case where we are deploying the sample workshop from within a workshop, and wouldn't always be used. We will dive further into defining the workshop settings later.

When run, the deployment script will create a deployment called `lab-sample-workshop`. The script will only return once the deployment has completed.

Now run:

```execute
oc get is -l app=lab-sample-workshop
```

You should see that an image stream has been created corresponding to the workshop image used in the deployment. By default the image stream is set up to use an image from `quay.io` for the original sample workshop content. We need to override that image with one built from our copy of the sample workshop content.

To do this, run:

```execute
.workshop/scripts/build-workshop.sh
```

This script will create a binary input build and push up the workshop content from the current directory, overriding the original sample workshop content from the image pulled from `quay.io`.

Once the build and re-deployment has finished, run:

```execute
oc get route lab-sample-workshop
```

This should show the hostname to access the newly deployed workshop content from your browser. In this case you should also be able to click on:

https://lab-sample-workshop-%project_namespace%.%cluster_subdomain%

You will be prompted to login. Use `workshop` for both the username and password.

The content displayed at this point is that for your copy of the sample workshop. This is where you would start modifying the content.
