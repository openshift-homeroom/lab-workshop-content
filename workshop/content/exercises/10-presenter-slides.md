---
Title: Presenter Slides
PrevPage: 09-index-ordering
NextPage: ../finish
---

If a workshop includes a presentation, slides can be included by placing them in the `workshop/slides` directory. Anything in this directory will be served up as static files via a HTTP web server. The default web page should be provided as `index.html`.

To support the use of [reveal.js](https://revealjs.com/), static media assets for that package are already bundled and available at the standard URL paths that the package expects. You should therefore be able to drop your slide presentation using reveal.js into the `workshop/slides` directory and it will work with no additional setup.

For slides bundled as a PDF file, add the PDF file to `workshop/slides` and then add an `index.html` which displays the PDF [embedded](https://stackoverflow.com/questions/291813/recommended-way-to-embed-pdf-in-html) in the page.

You can reference the slides from workshop content using <code>&percnt;slides_url&percnt;</code> as target of a link.

* [Slides](%slides_url%) - <code>&percnt;slides_url&percnt;</code>

If you are using reveal.js for the slides and you have history enabled, or are using section IDs to support named links, you can use an anchor to a specific slide and that specific slide will be opened.

* [Questions](%slides_url%#/questions) - <code>&percnt;slides_url&percnt;#/questions</code>

In both cases, when using embedded links to the slides in workshop content, if the workshop content is displayed as part of the dashboard, the slides will be opened in the tab to the right rather than as a separate browser window or tab.
