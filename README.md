LAB - Workshop Content
======================

This repository provides a workshop where you will learn how to create and structure the content for your own workshop. You will also learn how to deploy your workshop content to be able to test it.

To deploy the workshop, first clone a copy of this Git repository to your own machine using the command:

```
git clone --single-branch --branch master --recurse-submodules https://github.com/openshift-homeroom/lab-workshop-content.git
```

Change the working directory to `lab-workshop-content`.

If you forgot to use the `--recurse-submodules` option when cloning the repository, run:

```
git submodule update --init --recursive
```

It is recommended you now create a new project into which to deploy the workshop. The same project will be used by the workshop as it steps you through the different ways workshops can be deployed. When finished, you can delete the whole project to have everything removed.

```
oc new-project workshop
```

Now deploy the workshop by running:

```
.workshop/scripts/deploy-personal.sh
```

The output from the script will show the host name to access from your web browser. You can also see the host name by running:

```
oc get routes lab-workshop-content
```

Access to the workshop environment will be password protected and you will see a browser popup for entering user credentials. The username to enter is `workshop`. The password will also be `workshop`.

When you are finished you can delete the project you created.

If you didn't follow the recommendation of using a new project, and instead used an existing project, run:

```
.workshop/scripts/delete-personal.sh
```

Note that this will not delete anything which may have been deployed when you went through the workshop. If you used an existing project, ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make.
