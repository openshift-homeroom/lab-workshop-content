---
Title: Share Workshops
PrevPage: 12-asciidoc-support
NextPage: 14-deploy-workshops
---

Workshops are shared by building the content, and any additional files or software, into a container image. The container image would then be hosted on an image registry such as Quay.io or Docker Hub.

In this workshop, the container image for the workshop was built in OpenShift using a `docker` type build. You could also use the `docker` or `buildah` command line tools to build it on your own local computer and push the resulting image up to an image registry. Services such as Quay.io, which provide the means to build container images from a hosted Git repository could also be used. If there is no requirement to be able to add steps to the `Dockerfile` which run as the `root` user, the `s2i` command line tool could also be used by using the `workshop-dashboard` base image as an S2I builder image.
