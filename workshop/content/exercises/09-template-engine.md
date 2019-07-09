All content in a page will be displayed. If you need to have content which should only be displayed if certain data variables are set, or need to be able to use some other type of conditional logic, you can optionally enable use of the [Liquid](https://www.npmjs.com/package/liquidjs) template engine.

To enable this, add the `config.template_engine` field to the modules configuration file.

```
config:
    template_engine: liquid.js
```

This will allow you to use the syntax implemented by the Liquid template engine.

```
{% if LANGUAGE == 'java' }
....
{% endif %}
{% if LANGUAGE == 'python' }
....
{% endif %}
```

Note that when enabling the template engine, the way you make use of data variables changes.

Instead of use the `%` character to enclose the name of the data variable you want inserted, you need to use the Liquid convention for referencing data variables. That is, `{{ LANGUAGE }}`.
