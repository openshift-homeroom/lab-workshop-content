In this workshop we built the image for the workshop in OpenShift. You can also use `docker` or `buildah` on your local computer.

Building the image locally can result in faster turn around times on builds than building it in OpenShift or using separate CI/CD infrastructure.

Even though the image is being built locally, and is principally designed to be run in OpenShift, you can still run it with your local container run time. In doing this you will not have access to the embedded web console, and you will need to manually login to any remote OpenShift cluster from the terminal before going through the workshop, but everything else should still work.

To build the workshop image locally using `docker` you would run:

```
docker build -t lab-sample-workshop .
```

To run the image, you would then use:

```
docker run --rm -p 10080:10080 lab-sample-workshop
```

You can then access the workshop environment using `http://localhost:10080`.

If you want to be able to do iterative changes and test them without needing to rebuild the image each time, you can run:

```
docker run --rm -p 10080:10080 -v `pwd`:/opt/app-root/src lab-sample-workshop
```

This will mount your local Git repository directory into the container and the local files will be used. Each time you change the content of a page, refresh the web browser to view the latest version. You will only need to stop and restart the container if you make changes to the YAML configuration files or the `config.js` file if you are using it.

If using this method of mounting your local Git repository into the container, if the steps performed in the workshop result in modifications to files under version control, make sure you don't subsequently commit those changes. Instead, you will need to make sure you rollback such changes each time you want to run through the steps in the workshop.
