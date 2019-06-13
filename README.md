LAB - Workshop Content
======================

This repository provides sample content for a workshop that can be used as the starting point for your own workshop. The sample content when deployed, will guide you through how to use the sample content, what the various directories and files are for, and how to format the contents of files.

To deploy the sample workshop, it is recommended you first create a fresh project into which to deploy it. The same project will then be used by the workshop as it steps you through the different ways workshops can be deployed.

```
oc new-project labs
```

In the active project you want to use, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/openshiftlabs/lab-workshop-content:1.1" \
  --param APPLICATION_NAME=sample-workshop
```

To get the hostname for the sample workshop, run:

```
oc get route sample-workshop
```

Use your browser to access the sample workshop.

You may need to supply your login/password again for the OpenShift cluster you deployed the sample workshop to. You will only be able to access it if you are a project admin of the project it is deployed to.

When you are finished you can delete the project you created, or if you used an existing project, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=sample-workshop
```

Note that this will not delete anything which may have been deployed when you went through the sample workshop. Ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make.
