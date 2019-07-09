The purpose of a workshop is to guide users through a set of steps to run, where different sections are maintained as different pages. The order in which pages are traversed, is dictated by the order in which modules are listed under the `modules.activate` field in the workshop configuration file. The order in which modules appear in the modules configuration file is not relevant.

```
name: Markdown Sample

modules:
    activate:
    - workshop-overview
    - setup-environment
    - exercises/01-sample-content
    - workshop-summary
```

If you need to run more than one variant of the workshop, you can provide more than one workshop configuration file, each activating a different set of modules, and select which should be used using the `WORKSHOP_FILE` environment variable.

At the bottom of each page a "Continue" button will be displayed to go to the next page in sequence. The label for this button can be customised if necessary, by setting the `exit_sign` field in the entry for the module in the modules configuration file.

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

For the last module in the workshop, a button will still be displayed, but where the user is taken when the button is pressed can vary.

If you want the user to be taken to a different web site upon completion, always leaving the workshop environment in its current state, you can set the `exit_link` field of the final module to the external URL.

When a workshop session is being created by the workshop spawner, it will inject its own special URL for the exit link via the `RESTART_URL` environment variable. When the user clicks on the final button in this case, the current workshop environment will be shutdown and the user will be redirected back to the start of the workshop, with a new workshop environment being created, or back to a page where they can pick which workshop they want to do next.

If the `exit_link` field is not defined, nor does a spawner inject a URL to start over, the user will be redirected back to the starting page of the workshop, leaving the current workshop environment intact.

The recommendation is that for the last page, the `exit_sign` be set to `Finish Workshop` and `exit_link` not be specified. This way the spawner for the workshop can control what happens when the user is finished.
