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
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param APPLICATION_NAME=lab-sample-workshop \
  --param AUTH_USERNAME=workshop \
  --param AUTH_PASSWORD=$AUTH_PASSWORD
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

You should see that an image stream has been created corresponding to the workshop image used in the deployment. By default the image stream is set up to use the workshop dashboard image base class. This image will use some dummy workshop content used when testing. We need to substitute that image with one built from our sample workshop content.

To do this, create a new build of type binary.

```execute
oc new-build --name lab-sample-workshop --binary
```

Now trigger a build, using the files from then current directory.

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

You will be prompted to enter a login and password. Use `workshop` for the login name. The password was set to the same value you used to access this initial workshop environment. If you have forgotten what that was, run:

```execute
oc set env dc/lab-sample-workshop --list | grep AUTH_PASSWORD
```

Right now the content displayed is the same as this workshop. This is where you would start modifying the content.
