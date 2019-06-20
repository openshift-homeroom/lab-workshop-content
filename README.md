LAB - Workshop Content
======================

This repository provides sample content for a workshop that can be used as the starting point for your own workshop. The sample content when deployed, will guide you through how to use the sample content, what the various directories and files are for, and how to format the contents of files.

To deploy the sample workshop, it is recommended you first create a fresh project into which to deploy it. The same project will then be used by the workshop as it steps you through the different ways workshops can be deployed.

```
oc new-project labs
```

In the active project you want to use, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/2.14.4/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/openshiftlabs/lab-workshop-content:1.2" \
  --param APPLICATION_NAME=lab-workshop-content \
  --param AUTH_USERNAME=workshop
```

Access to the workshop environment will be password protected and you will see a browser popup for entering user credentials. The username to enter is `workshop`. The password is displayed in the output from deploying the workshop environment, but can also be queried by running:

```
oc set env --list dc/lab-workshop-content | grep AUTH_PASSWORD
```

With the password in hand, the hostname for accessing the sample workshop environment in your browser can be found by running:

```
oc get route lab-workshop-content
```

When you are finished you can delete the project you created, or if you used an existing project, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=lab-workshop-content
```

Note that this will not delete anything which may have been deployed when you went through the sample workshop. Ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make. Alternatively, if you deploy the workshop environment in a fresh project, delete the project.
