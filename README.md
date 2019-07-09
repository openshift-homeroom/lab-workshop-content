LAB - Workshop Content
======================

This repository provides a work where you will learn how to create and structure the content for your own workshop. You will also learn how to deploy your workshop content to be able to test it.

It is recommended you create a new project into which to deploy the workshop. The same project will then be used by the workshop as it steps you through the different ways workshops can be deployed.

```
oc new-project labs
```

In the active project you want to use, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/3.3.3/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/openshifthomeroom/lab-workshop-content:1.4" \
  --param APPLICATION_NAME=lab-workshop-content \
  --param AUTH_USERNAME=workshop \
  --param AUTH_PASSWORD=workshop
```

Access to the workshop environment will be password protected and you will see a browser popup for entering user credentials. The username to enter is `workshop`. The password will also be `workshop`.

You can use a different password by changing the value passed to the `AUTH_PASSWORD` template parameter.

The hostname for accessing the workshop environment in your browser can be found by running:

```
oc get route lab-workshop-content
```

When you are finished you can delete the project you created..

If you didn't follow the recommendation of using a new project, and instead used an existing project, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=lab-workshop-content
```

Note that this will not delete anything which may have been deployed when you went through the workshop. If you used an existing project, ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make.
