---
Title: Data Variables
PrevPage: 05-page-formatting
NextPage: 07-embedded-links
---

When creating page content, you can reference a number of pre-defined data variables. The values of the data variables will be substituted into the page when rendered in the users browser.

The workshop environment provides the following built-in data variables.

* `username` - The identity of the user doing the workshop. This will usually only be set when the workshop is deployed in a multi user deployment. This is different from the name of the service account the workshop environment is running as.
* `project_namespace` - The name of the OpenShift project the workshop environment is linked to and into which any deployed applications will run. Depending on how the workshop has been deployed, this may be the same project the workshop environment is running in, or may be a distinct project created for the workshop in advance.
* `cluster_subdomain` - The subdomain used in generated route hostnames of applications deployed to the OpenShift cluster.
* `base_url` - The root URL for the workshop content.
* `terminal_url` - The root URL for the terminal application.
* `console_url` - The root URL for the embedded web console.
* `slides_url` - The root URL for the slides if provided.

To use a data variable within the page content, surround it each side with `%`.

<pre><code>%username%</code><pre/>

This can be done inside of code blocks, as well as in URLs.

<pre><code>http://sample-%project_namespace%.%cluster_subdomain%/</code><pre/>

For the way in which this workshop has been deployed, the values of these variables are:

* username: %username%
* project_namespace: %project_namespace%
* cluster_subdomain: %cluster_subdomain%
* base_url: %base_url%
* console_url: %console_url%
* terminal_url: %terminal_url%
* slides_url: %slides_url%
