---
Sort: 2
Title: Workshop Setup
PrevPage: index
NextPage: exercises/01-workshop-template
ExitSign: Start Workshop
---

In a workshop, the first thing you usually want to do is ensure that the workshop environment is installed correctly. Exactly what you should provide in this step will depend on whether the workshop is designed to be deployed in a specific way.

For this sample workshop, it is enough to check that you are logged in correctly and will be able to deploy applications. To do this run:

```execute
oc auth can-i create pods
```

Did you type the command in yourself? If you did, click on the command instead and you will find that it is executed for you. You can click on any command which has the <span class="glyphicon glyphicon-play-circle"></span> icon shown to the right of it, and it will be copied to the interactive terminal and run.

If the output from the `oc auth can-i` command is `yes`, you are all good to go, and you can scroll to the bottom of the page and click on "Start Workshop".

If instead of the output `yes`, you see:

```
no - no RBAC policy matched
```

or any other errors, then the environment is not deployed correctly. Check the [GitHub repository](https://github.com/openshift-labs/workshop-content) for this sample workshop for details of how to deploy it.

For a more elaborate example of what you might supply for this step, where trying to support standalone deployment by a single user, use in a hosted workshop, or as part of a learning portal, see the [setup instructions](https://github.com/jupyter-on-openshift/lab-jupyter-notebooks-01/blob/master/workshop/content/setup.md) for the workshop on deploying Jupyter notebooks to OpenShift.

Ensure you look at the raw view of the content so you can see the markup being used. We will talk more about formatting the content later.
