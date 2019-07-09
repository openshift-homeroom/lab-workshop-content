The recommended approach to distribute a workshop is to create a container image which packages up your workshop. This way, the workshop content, along with all the command line tools, runtime language environments and applications used to display the workshop content are together.

You can use `docker` or `buildah` to build the image using the supplied `Dockerfile`. If you have no need to install extra system packages, you could also use Source-to-Image (S2I) to build the image as the base image used in a `docker` type build, can also be used as an S2I builder.

In this workshop the ability to build the image using the `Dockerfile` will be used. Rather than use `docker` or `buildah`, we will setup a build configuration in OpenShift, pushing the workshop content using a binary input build.

Before we set up the build, we will create a deployment for the workshop environment. To do this run:

```execute
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param APPLICATION_NAME=lab-sample-workshop \
  --param AUTH_USERNAME=workshop \
  --param AUTH_PASSWORD=workshop
```

This will create a deployment called `lab-sample-workshop`. Run:

```execute
oc rollout status dc/lab-sample-workshop
```

to monitor the progress of the deployment.

Now run:

```execute
oc get is -l app=lab-sample-workshop
```

You should see that an image stream has been created corresponding to the workshop image used in the deployment. By default the image stream is set up to use the workshop dashboard image base class. This image will use some dummy workshop content used when testing. We need to substitute that image with one built from our workshop content.

To do this, we are going to create a build configuration in OpenShift for a `docker` type build. The build will be created as a binary input build so we can inject the source code for the build from the local directory.

To create the binary input build configuration run:

```execute
oc new-build --name lab-sample-workshop --binary --strategy docker
```

The name used for the build needs to be the same as the image stream above.

Now trigger a build, using the files from the current directory.

```execute
oc start-build lab-sample-workshop --from-dir . --follow
```

Once the build has complete, wait for the new deployment using this image:

```execute
oc rollout status dc/lab-sample-workshop
```

Then run:

```execute
oc get route lab-sample-workshop
```

This should show the hostname to access the newly deployed workshop content from your browser. In this case you should also be able to click on:

https://lab-sample-workshop-%project_namespace%.%cluster_subdomain%

You will be prompted to login. Use `workshop` for both the username and password.

The content displayed at this point is that for the sample workshop. This is where you would start modifying the content.
