URLs can be included in workshop content. This can be the literal URL, or the Markdown syntax for including and labelling a URL. What happens when a user clicks on a URL, will depend on the specific URL.

In the case of the URL being an external web site, when the URL is clicked, the URL will be opened in a new browser tab or window.

* [External](https://www.openshift.com)

When the URL is a relative page referring to another page which is a part of the workshop content, the page will replace the current workshop page.

* [Internal](08-embedded-links)

A URL can be provided using a data variable. This could be one of the builtin data variables, or one you have added to the workshop config.

You can also define a URL where components of the URL are provided by data variables. Data variables useful in this content are `project_namespace` and `cluster_subdomain` as they can be used to create a URL to an application deployed from a workshop.

* [Application](https://lab-sample-workshop-%project_namespace%.%cluster_subdomain%) - <code>https&colon;//lab-sample-workshop-&percnt;project_namespace&percnt;.&percnt;cluster_subdomain&percnt;</code>

A number of the builtin data variables which provide a URL path value are treated in a special way when clicked.

* `terminal_url` - When clicked the terminal tab will be selected and brought to the front if not already visible.
* `console_url` - When clicked the console tab will be selected and brought to the front if not already visible.
* `slides_url` - When clicked the slides tab will be selected and brought to the front if not already visible.

In the case of `terminal_url`, you can append a path to the URL identifying a specific terminal session. In this case a new browser tab or window will be opened on that session.

* [Terminal](%terminal_url%) - <code>&percnt;terminal_url&percnt;</code>
* [Session](%terminal_url%/session/3) - <code>&percnt;terminal_url&percnt;/session/3</code>

In the case of `console_url`, you can append a path to the URL, and the console tab, as well as being brought to the front if not already visible, will be opened on the given URL path.

* [Projects](%console_url%) - <code>&percnt;console_url&percnt;</code>
* [Status](%console_url%/overview/ns/%project_namespace%) - <code>&percnt;console_url&percnt;/overview/ns/&percnt;project_namespace&percnt;</code>
* [Events](%console_url%/k8s/ns/%project_namespace%/events) - <code>&percnt;console_url&percnt;/k8s/ns/&percnt;project_namespace&percnt;/events</code>
* [Pods](%console_url%/k8s/ns/%project_namespace%/pods) - <code>&percnt;console_url&percnt;/k8s/ns/&percnt;project_namespace&percnt;/pods</code>

In the case of `slides_url`, the slides will be brought to the front if not already visible. If you are using reveal.js for the slides and you have history enabled, or are using section IDs to support named links, you can use an anchor to a specific slide and that specific slide will be opened.

* [Slides](%slides_url%) - <code>&percnt;slides_url&percnt;</code>
* [Questions](%slides_url%#/questions) - <code>&percnt;slides_url&percnt;#/questions</code>
