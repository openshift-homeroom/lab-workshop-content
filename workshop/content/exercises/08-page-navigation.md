---
Title: Page Navigation
PrevPage: 07-embedded-links
NextPage: 09-index-ordering
---

The purpose of a workshop is to guide users through a set of steps they are to run, where different sections are maintained as different pages. To set up the overall path a user needs to follow, you need to specify the page navigation path. This is done by defining what are the previous and next pages relative to a page as fields in the page meta data. In addition to linking the pages, you can customise the label used on the button displayed at the bottom of each page, for the outgoing page link.

The meta data for this page is:

```
---
Title: Page Navigation
PrevPage: 07-embedded-links
NextPage: 09-index-ordering
---
```

The `Title` field sets the title for the page. If this is not defined the title of the page will default to a title constructed from the name of the file.

The `PrevPage` and `NextPage` fields are used to define the name of the previous and next pages in the navigation path. This name is the name of the file for the page, without the `.md` file extension.

In this workshop, the main pages containing the steps the user is to run, are located in an `exercises` sub directory, with the logical navigation page being as follows.

```
index.md
setup.md
exercises/01-sample-workshop.md
exercises/02-directory-layout.md
exercises/03-building-image.md
exercises/04-workshop-config.md
exercises/05-page-formatting.md
exercises/06-data-variables.md
exercises/07-embedded-links.md
exercises/08-page-navigation.md
exercises/09-index-ordering.md
exercises/10-presenter-slides.md
exercises/11-build-and-setup.md
exercises/12-asciidoc-support.md
exercises/13-share-workshops.md
exercises/14-deploy-workshops.md
finish.md
```

When referring to a page in the same directory, you would use just the name of the page. If you needed to refer to a page in a subdirectory, prefix the name with the directory as a path. For example, the `setup.md` page contained:

```
---
Sort: 2
Title: Workshop Setup
PrevPage: index
NextPage: exercises/01-sample-workshop
ExitSign: Start Workshop
---
```

To refer to a page in a parent directory, use `..`. For example, the `exercises/14-deploy-workshops.md` page contained:

```
---
Title: Deploy Workshops
PrevPage: 13-share-workshops
NextPage: ../finish
---
```

The `ExitSign` field that was used in the `setup.md` page overrides the label displayed on the button at the bottom of the page, for going to the next page. If the `ExitPage` field is not specified, the label on the button will default to `Continue`.

If the `ExitSign` field is included but `NextPage` is not defined, the page is treated as the last page in the navigation path. A button will still be displayed, but where the user is taken when the button is pressed can vary.

If you want the user to be taken to a different web site upon completion, always leaving the workshop environment in its current state, you can set the `ExitLink` field to the URL.

When a workshop session is being created by the workshop spawner, it will inject its own special URL for the exit link via the `RESTART_URL` environment variable. When the user clicks on the button in this case, the current workshop environment will be shutdown and the user will be redirected back to the start of the workshop, with a new workshop environment being created, or back to a page where they can pick which workshop they want to do next.

If the `ExitLink` field is not defined, nor does a spawner inject a URL to start over, the user will be redirected back to the starting page of the workshop, leaving the current workshop environment intact.

The recommendation is that for the last page, the `ExitSign` be set to `Finish Workshop` and `ExitLink` to not be specified. This way the spawner for the workshop can control what happens when the user is finished. For example, for this workshop, the final `finish.md` page contained:

```
---
Sort: 3
Title: Workshop Summary
PrevPage: exercises/14-deploy-workshops
ExitSign: Finish Workshop
---
```

When defining the page navigation path, always include `PrevPage` on all pages except for the first page. This ensures a user can go backwards by clicking on the arrows at the top of a page. If not included, they will need to right click in the browser frame and select `Back`, or for some browsers they may be able to use the main browser back button.

As to the structure of the pages and the use of the `exercises` directory for the main workshop content, with numbered files within, and with top level `index.md`, `setup.md` and `finish.md` pages, only the `index.md` file must exist. This is the initial starting page for the workshop content.

Although this is a page structure we have found that works well, you could ignore it and place all pages in the top level directory. The important part is that you define the page navigation path, using the meta data fields of each page. Depending on how you name files, you may also need to indicate page ordering for when pages are display in the generated page index.

By using a sub directory to group the main pages, it would allow you to have multiple sub directories corresponding to different parts of a longer workshop. You could set up the page navigation so the users progress from one part of the workshop to the next, or direct them back to a top level page, and use a list of links, possibly using custom buttons defined using embedded HTML markup, to select which part they want to do. This approach might be used to allow them to select a variant of the workshop content where a different programming language was used, where pages for each different language were in separate directories.
