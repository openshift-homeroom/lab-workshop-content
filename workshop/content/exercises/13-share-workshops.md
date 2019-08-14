Workshops are shared by building the content, and any additional files or software, into a container image. The container image would then be hosted on an image registry such as Quay.io or Docker Hub.

In this workshop, the container image for the workshop was built in OpenShift using a `docker` type build. You could also use the `docker` or `buildah` command line tools to build it on your own local computer and push the resulting image up to an image registry.

Services such as Quay.io, which provide the means to build container images from a hosted Git repository could also be used

If there is no requirement to be able to add steps to the `Dockerfile` which run as the `root` user, the `s2i` command line tool could also be used by using the `workshop-dashboard` base image as an S2I builder image.

If you have built your workshop into an image and are hosting it on an image registry that would be accessible to whoever wants to run the workshop, you can update the `.workshop/settings.sh` file with its location.

```execute
cat .workshop/settings.sh
```

Change the `WORKSHOP_IMAGE` variable to be the name that identifies where your image is being made available.

When this is defined and part of your Git repository, when the `deploy-personal.sh` script is run to deploy the workshop, it will pull down and use your image. There will be no need to run `build-workshop.sh` to build the image for the workshop from the local source files from the Git repository.

To ensure that a specific version of the workshop is being used, rather than the latest version which may be in a state of development, you can when setting `WORKSHOP_IMAGE` reference a specific version tag.
