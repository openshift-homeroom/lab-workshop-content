From the output of initially running `git commit` with the sample workshop content, you will have seen a number of files located in the top level directory, and a number of sub directories forming a hierarchy.

The files in the top level directory are:

* `README.md` - A file telling everyone what the workshop in your Git repository is about, and how to deploy it. Replace the current content provided in the sample workshop with your own.
* `LICENSE` - A license file so people are clear about how they can use your workshop content. Replace this with what license you want to apply to your workshop content.
* `Dockerfile` - The steps to build your workshop into an image ready for deployment. This would be left as is, unless you want to customize it to install additional system packages.

Key sub directories and the files contained within them are:

* `workshop` - Directory under which your workshop files reside.
* `workshop/modules.yaml` - Configuration file with details of available modules which make up your workshop, and data variables for use in content.
* `workshop/workshop.yaml` - Configuration file which provides the name of the workshop, the list of active modules for the workshop, and any overrides for data variables.
* `workshop/content` - Directory under which your workshop content resides, including images to be displayed in the content.
* `.workshop/build` - A script in which you can specify steps to be run when the image for your workshop is built.
* `.workshop/setup` - A script in which you can specify steps to be run each time the container your workshop is deployed into starts.
* `.workshop/settings.sh` - A settings file which describes attributes of the workshop, for when using the workshop scripts to deploy the workshop.
