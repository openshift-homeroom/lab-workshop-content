When building the container image for a workshop, you can include any additional files that may be required to do the workshop. This can include source code files or scripts. The supplied `Dockerfile` will ensure that these files are copied into the home directory for the workshop environment. This is the same directory used as the working directory for the embedded terminals.

If you need to perform any extra steps during the build process for the container image, you can add these steps to the executable `.workshop/build` script file.

The default build script used in the sample workshop is:

```
#!/bin/bash

# This 'build' script is where you can add steps that should be run when
# building the image for your custom workshop.

# Move the workshop content to '/opt/app-root/workshop'. It could be left
# at it's default location of '/opt/app-root/src/workshop', but by moving it,
# it is out of view of the user doing the workshop and they aren't likely to
# delete it by accident and break the display of the workshop content.

mv workshop /opt/app-root/workshop

# Also delete some of the other files from the top of the Git repository we
# don't need for running the workshop.

rm -f Dockerfile README.md LICENSE

# If the workshop requires Git, it is necessary to set some defaults for
# the name and email of the user for Git.

git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

This can be used to perform tasks like remove any extra files which are not needed for the workshop and which may confuse users were they present. If the workshop uses Git, you can set any global options required to configure Git which are not dependent on a specific session. You could also checkout copies of remote Git repositories, download any other required files or application source code, and build any applications.

One special step you can add to the build script is to move the complete `workshop` directory containing the workshop content and slides, to the `/opt/app-root/workshop` directory. This is an alternate location for placing the workshop content. By moving this, it will not be visible to the user in the home directory which lessons the risk of them removing it and breaking the rendering of the workshop content.

Because the build script is run as a non privileged user, you cannot add steps to this script which need to run as the `root` user, such as install system packages. If you need to run any steps as the `root` user, you will need to add these to the `Dockerfile` and be using a `docker` type build and not an S2I build.

When the container image for the workshop is deployed, if you need to run extra steps which depend on the workshop environment for a specific session, you can add them to the executable `.workshop/setup` script. As with the build script, this is run as a non privileged user.

The setup script will be run before the web application which provides the workshop environment dashboard. Any steps you add will therefore block the start up of the workshop environment. You should avoid doing anything which takes a non trivial amount of time.

Where the deployment method for a workshop environment automatically logs in the user to the OpenShift cluster, the setup script can be used to run commands against the OpenShift cluster. This could include pre-deploying applications on behalf of the user. Any such actions must though be tolerant of being run more than once, as they may be run a further time were the container to be restarted.
