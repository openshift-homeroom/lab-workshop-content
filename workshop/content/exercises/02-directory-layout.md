---
Title: Directory Layout
PrevPage: 01-sample-workshop
NextPage: 03-building-image
---

From the directory listing you ran, you will see a number of files located in the top level directory, and a number of sub directories forming a hierarchy.

The files in the top level directory are:

* `README.md` - A file telling everyone what the workshop in your Git repository is about, and how to deploy it. Replace the current content provided in the sample workshop with your own.
* `LICENSE` - A license file so people are clear about how they can use your workshop content. Replace this with what license you want to apply to your workshop content.
* `Dockerfile` - The steps to build your workshop into an image ready for deployment. This would be left as is, unless you want to customize it to install additional system packages.

Key sub directories and files contained within them are:

* `workshop` - Directory under which your workshop files reside.
* `workshop/config.js` - Configuration file for setting the workshop title, data analytics trackers, and custom data variables.
* `workshop/content` - Directory under which your workshop content, including images to be displayed in the content, resides.
* `workshop/slides` - Directory under which you can optionally provide a set of slides if your workshop incorporates a presentation.
* `.workshop/build` - A script in which you can specify steps to be run when the image for your workshop is built.
* `.workshop/setup` - A script in which you can specify steps to be run each time the container your workshop is deployed into starts.
* `.s2i/environment` - Environment variables to be set for your workshop image if using Source-to-Image (S2I) to build the image, rather than building using the `Dockerfile`.
