The aim for a workshop is to provide an interactive environment where users will run the steps covered by the workshop content in their own session.

If you need to host online a permanently available copy of the workshop content, but without the interactive environment, you can use the `deploy-personal.sh` script, but override the `DASHBOARD_MODE` settings with the value `workshop-only`.

```
.workshop/scripts/deploy-personal.sh --override DASHBOARD_MODE=workshop-only
```

The workshop content will be displayed full screen, without the dashboard, or any access to the terminal, embedded web console, or slides.

Where the workshop content marks code blocks as executable, when in full screen mode, they will be shown instead as blocks which when clicked, will be copied to the browser paste buffer.

If desired, you can create a separate settings file with this setting, and use the `--settings` option to refer to it.
