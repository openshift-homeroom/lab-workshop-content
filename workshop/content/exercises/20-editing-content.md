Now that you have gone through this workshop, you can download the sample workshop you want to use as a starting point for your own workshop. Delete the pages under the `workshop/content/exercises` directory in your copy, add your own pages, and update the workshop and modules configuration files, as well as the deployment settings file.

When editing your workshop content on your local computer, you can use editors such as Atom and VSCode. Because images are placed in the same directory as the markdown files, preview modes of these editors will work, including the embedded images, and you can see what your content should look like without needing to first deploy it.

It is recommended you use such editors with a preview mode, as it means you can make a whole batch of changes and see what it looks like before needing to build a new image containing the content and deploy it, to test any steps.

Do be aware that these editors no not know anything about the annotations added to code blocks, so you will not get any visual indicators of where you have applied them. Data variables will also not be expanded, nor any template logic if the template engine is enabled. It is possible that template logic may interfere with any live preview feature of the editors.
