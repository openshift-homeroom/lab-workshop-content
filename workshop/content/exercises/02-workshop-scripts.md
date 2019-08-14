In order to make deployment of a workshop easier, for both personal use and if running a multi user workshop, a set of deployment scripts are provided which wrap up all the steps required to deploy the workshop. These scripts are supplied as part of the Git repository:

* https://github.com/openshift-homeroom/workshop-scripts

To use the scripts with your workshop, they should be included into your Git repository as a Git submodule. This is done, rather than making a copy of the files into your Git repository, so it is easier to update your workshop to the latest scripts at any time.

Once you have setup the Git repository for your own workshop using one of the sample workshops as a starting point, to add the workshop scripts, run the following commands:

```execute
rmdir .workshop/scripts
```

This removes the `.workshop/scripts` directory that may exist when unpacking the sample workshop.

Next configure Git to add the `workshop-scripts` Git repository as a Git submodule:

```execute
git submodule add -b stable/1.x https://github.com/openshift-homeroom/spawner-scripts.git .workshop/scripts
```

Then checkout a copy of the Git submodule:

```execute
git submodule update --remote
```

You should see that the `.workshop/scripts` directory now contains a number of different scripts and files.

```execute
ls -las .workshop/scripts
```

One of these files is the `default-settings.sh` file. View the contents by running:

```execute
cat .workshop/scripts/default-settings.sh
```

This file includes variables which indicate what versions of the workshop images should be used when using this version of the workshop scripts. The one we are interested in at this point is the `DASHBOARD_IMAGE` variable.

This indicates the version of the workshop dashboard base image which should be used. This needs to match what is used in the `FROM` statement of the `Dockerfile` in the current directory, used to build your workshop:

```execute
cat Dockerfile
```

Edit the `Dockerfile` if the image is different and set it to the required version, or run:

```execute
(. .workshop/scripts/default-settings.sh; sed -i -e "s%^FROM .*$%FROM $DASHBOARD_IMAGE%" Dockerfile)
```

As well as the change to the `Dockerfile`, it is also necessary to edit the `.workshop/settings.sh` file. This file contains the name used for the workshop deployment.

```execute
cat .workshop/settings.sh
```

The `WORKSHOP_NAME` variable should be changed to `lab-sample-workshop`, to match the name used for the Git repository directory.

```execute
sed -i -e "s/^WORKSHOP_NAME=.*$/WORKSHOP_NAME=lab-sample-workshop/" .workshop/settings.sh
```

When both changes have been made, add all the changes to your Git repository:

```execute
git add .
```

and commit the changes:

```execute
git commit -m 'Add workshop scripts submodule.'
```

If in the future you want to update the version of the workshop scripts used with your workshop, run again the `git submodule update --remote` command. Then update the version of the dashboard base image in the `Dockerfile` to match.
