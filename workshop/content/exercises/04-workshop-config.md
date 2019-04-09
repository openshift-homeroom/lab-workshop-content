---
Title: Workshop Config
PrevPage: 03-building-image
NextPage: 05-page-formatting
---

The first change you will want to make is to set the title for your workshop. This is what appears in the banner at the top of content in the left side of the workshop dashboard.

This change can be made in the `workshop/config.js` file. This file is used to set the workshop title, add a data analytics tracking code, and set custom data variables.

The config file is Javascript code. The format of the file is:

```
var google_analytics = `
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-135921114-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-XXXXXXXXX-1');
</script>
`;

var config = {
    site_title: 'Workshop Content',

    // analytics: google_analytics,

    variables: [
        {
            name: 'name',
            content: 'value'
        }
    ]
};

module.exports = config;
```

The `config` variable is a Javascript dictionary in which configuration settings are added. The key settings are:

* `site_title` - The title of your workshop. Keep this short as there is only limited space when content is displayed in the dashboard along side the terminal. If the title is too long it will be wrapped.
* `analytics` - The analytics data tracking code for any service you want to use to track usage of your workshop.
* `variables` - A list of custom data variables which will be available for use in the content of your pages. We will cover how to use data variables later.

Change the `site_title` variable to a value which describes what your workshop is about. For this workshop, change it to `Custom Content`. You can use `vi` or `nano` in the terminal, or you can run:

```execute
sed -i -e 's/Workshop Content/Custom Content/' workshop/config.js
```

Having made a change, you can rebuild your custom image by running again:

```execute
oc start-build --from-dir . --follow
```

Once complete, [refresh the page](https://custom-%project_namespace%.%cluster_subdomain%) for your custom workshop to check the change works.


If you were happy with the change, you would then go onto adding and committing the change to your Git repository. This modify/re-build/re-fresh process is how you would go about working on your content and testing it.
