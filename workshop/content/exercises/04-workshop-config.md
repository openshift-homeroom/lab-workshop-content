There are different ways you can setup configuration for a workshop. The way used in the sample workshops is through YAML files.

The `workshop/modules.yaml` file provides details of available modules which make up your workshop, and data variables for use in content.

In the case of the list of modules, not all modules may end up being used. This is because this list represents the full set of modules you have available and might use. You may want to run variations of your workshop, such as for different programming languages. As such, which modules are active and will be used for a specific workshop are listed in the separate `workshop/workshop.yaml` file, along with the name to be given to the workshop when using that set of modules.

By default the `workshop.yaml` file will be used to drive what modules are used. Where you do have variations as to what content should be used, you can provide multiple workshop files with different names. You might for example instead provide `workshop-java.yaml` and `workshop-python.yaml`.

Where you have multiple workshop files, and don't have the default `workshop.yaml` file, you can specify the default workshop file to use by setting the `WORKSHOP_FILE` environment variable in the `Dockerfile`, to the name of the workshop file. The environment variable will be able to be overridden for a deployment to select a different workshop file when necessary.

The format for listing the available modules in the `workshop/modules.yaml` file is:

```
modules:
    workshop-overview:
        name: Workshop Overview
        exit_sign: Setup Environment
    setup-environment:
        name: Setup Environment
        exit_sign: Start Workshop
    exercises/01-sample-content:
        name: Sample Content
    workshop-summary:
        name: Workshop Summary
        exit_sign: Finish Workshop
```

Each available module is listed under `modules`, where the name used corresponds to the path to the file containing the content for that module, with any extension identifying the content type left off.

For each module, set the `name` field to the title to be displayed for that module. If no fields are provided and `name` is not set, the title for the module will be calculated from the name of the module file. The purpose of the `exit_sign` field will be discussed later when looking at page navigation.

The corresponding `workshop/workshop.yaml` file, where all available modules were being used, would have the format:

```
name: Markdown Sample

modules:
    activate:
    - workshop-overview
    - setup-environment
    - exercises/01-sample-content
    - workshop-summary
```

The top level `name` field in this file is the title to be displayed for the complete workshop. It will be shown in the banner for the workshop content when viewing the workshop environment in your web browser.

The `modules.activate` field is a list of modules to be used for the workshop. The names in this list must match the names as they appear in the modules file.

The first change you will want to make is to set the title for your workshop by changing the `name` field.

For this workshop, change it to `Sample Workshop`. You can use `vi` or `nano` in the terminal, or you can run:

```execute
sed -i -e 's/Markdown Sample/Sample Workshop/' workshop/workshop.yaml
```

Having made a change, you can rebuild the image and redeploy it by running:

```execute
oc start-build lab-sample-workshop --from-dir . --follow
```

Once the build has complete, wait for the new deployment using this image:

```execute
oc rollout status dc/lab-sample-workshop
```

Once complete, [refresh the page](https://lab-sample-workshop-%project_namespace%.%cluster_subdomain%) for your workshop to check the change works.

If you were happy with the change, you would then go onto adding and committing the change to your Git repository. This modify/build/refresh process is how you would go about working on your content and testing it.
