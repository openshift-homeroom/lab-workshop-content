When creating page content, you can reference a number of pre-defined data variables. The values of the data variables will be substituted into the page when rendered in the users browser.

The workshop environment provides the following built-in data variables.

* `username` - The identity of the user doing the workshop. This will usually only be set when the workshop is deployed in a multi user deployment. This is different from the name of the service account the workshop environment is running as.
* `project_namespace` - The name of the OpenShift project the workshop environment is linked to and into which any deployed applications will run. Depending on how the workshop has been deployed, this may be the same project the workshop environment is running in, or may be a distinct project created for the workshop in advance.
* `cluster_subdomain` - The subdomain used in generated route hostnames of applications deployed to the OpenShift cluster.
* `base_url` - The root URL path for the workshop content.
* `terminal_url` - The root URL path for the terminal application.
* `console_url` - The root URL path for the embedded web console.
* `slides_url` - The root URL path for slides if provided.

To use a data variable within the page content, surround it each side with the character `%`.

<pre><code>&percnt;username&percnt;</code></pre>

This can be done inside of code blocks, as well as in URLs.

<pre><code>http://lab-sample-workshop-&percnt;project_namespace&percnt;.&percnt;cluster_subdomain&percnt;/</code></pre>

For the way in which this workshop has been deployed, the values of these variables are:

* `username`: %username%
* `project_namespace`: %project_namespace%
* `cluster_subdomain`: %cluster_subdomain%
* `base_url`: %base_url%
* `console_url`: %console_url%
* `terminal_url`: %terminal_url%
* `slides_url`: %slides_url%

You can introduce your own data variables by listing them in the `workshop/modules.yaml` file. A data variable is defined as having a default value, but where the value will be overridden if an environment variable of the same name is defined.

The field under which the data variables should be specified is `config.vars`.

```
config:
    vars:
    - name: OC_VERSION
      value: undefined
    - name: KUBECTL_VERSION
      value: undefined
```

In this case, the `OC_VERSION` and `KUBECTL_VERSION` environment variables are set by the workshop environment. The values they have for this workshop are:

* `OC_VERSION`: %OC_VERSION%
* `KUBECTL_VERSION`: %KUBECTL_VERSION%

Where you want to use a name for a data variable which is different to the environment variable name, you can add a list of `aliases`.

```
config:
    vars:
    - name: LANGUAGE
      value: undefined
      aliases:
      - WORKSHOP_LANG
```

The environment variables with names given in the list of aliases will be checked first, then the environment variable with the same name as the data variable. If no environment variables with those names are set, then the default value will be used.

The default value for a data variable can be overridden for a specific workshop by setting it in the corresponding workshop file. For example, `workshop/workshop-python.yaml` might contain:

```
vars:
    LANGUAGE: python
```

If you need more control over setting the values of data variables, you can provide the file `workshop/config.js`. The form of this file should be:

```
function initialize(workshop) {
    workshop.load_workshop();

    if (process.env['WORKSHOP_FILE'] == 'workshop-python.yaml') {
        workshop.data_variable('LANGUAGE', 'python');
    }
}

exports.default = initialize;

module.exports = exports.default;
```

This Javascript code will be loaded and the `initialize()` function called to load the workshop configuration. You can then use the `workshop.data_variable()` function to set up any data variables

Because it is Javascript, you can write any code you need to query process environment variables and set data variables based on those. This might include creating composite values constructed from multiple environment variables. You could even download data variables from a remote host.
