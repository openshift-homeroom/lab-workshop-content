---
Title: Building Image
PrevPage: 02-directory-layout
NextPage: 04-workshop-config
---

A container image is used as the means to package up your workshop. This way, the workshop content, along with all the command line tools and runtime language environments are in the one package, with the applications used to display the workshop content and slides.

You can use `docker` or `buildah` to build the image using the supplied `Dockerfile`, or if you have no need to install extra system packages, you could also use Source-to-Image (S2I) to build the image.

In this workshop the ability to build the image using the `Dockerfile` will be used. Rather than use `docker` or `buildah`, we will setup a build configuration in OpenShift, pushing the workshop content using a binary input build.

Before we set up the build, we will create a deployment for the workshop environment. To do this run:

```execute
oc new-app workshop/deploy.json --param APPLICATION_NAME=custom-workshop
```

This will create a deployment called `custom-workshop`. Run:

```execute
oc rollout status dc/custom-workshop
```

to monitor the progress of the deployment.

Now run:

```execute
oc get is -l app=custom-workshop
```

You should see that an image stream has been created corresponding to the workshop image used in the deployment. By default the image stream is set up to use the workshop dashboard image base class. This image will use some dummy workshop content used when testing. We need to substitute that image with one built from our custom workshop content.

To do this, create a new build of type binary.

```execute
oc new-build --name custom-workshop --binary
```

Now trigger a build, using the files from then current directory.

```execute
oc start-build custom-workshop --from-dir . --follow
```

Once the build has complete, wait for the new deployment using this image:

```execute
oc rollout status dc/custom-workshop
```

Then run:

```execute
oc get route custom-workshop
```

This should show the hostname to access the newly deployed workshop content from your browser. In this case you should also be able to click on:

https://custom-workshop-%project_namespace%.%cluster_subdomain%

You will be prompted to enter a login and password. Use `workshop` for the login name. Use the password output when the deployment was created. You can also run:

```execute
oc set env dc/custom-workshop --list
```

to see the password. Use the value of the `AUTH_PASSWORD` environment variable set by the deployment.

Right now the content displayed is the same as this workshop. This is where you would start modifying the content.
