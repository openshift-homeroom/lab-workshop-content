To get you started with your own workshop content, a number of sample Git repositories are provided. Which you use will depend on whether you prefer to use Markdown or AsciiDoc formatting for content. These are:

* https://github.com/openshift-homeroom/lab-markdown-sample
* https://github.com/openshift-homeroom/lab-asciidoc-sample

You have two options for how you can get started with these sample Git repositories.

The first option is to use the GitHub feature for creating a new repository from a [Git repository template](https://help.github.com/en/articles/creating-a-repository-from-a-template). This is different to forking an existing Git repository on GitHub, in that it creates a fresh repository with the latest content from the original Git repository. In creating a Git repository using this feature, it does not inherit any commit history from the original, and it is not linked to the original. Once you have created your copy of the Git repository, you can check out a copy to your own machine and start working on it.

The second option is to download a copy of one of the sample Git repositories from the releases page for that Git repository. From this you can then create a local Git repository, and push it up to a Git repository hosting service of your choice.

In this workshop we will use the second option of downloading a copy of the sample Git repository from the GitHub releases archive.

To download the sample workshop using Markdown formatting, run:

```execute
curl -sL -o /tmp/lab-markdown-sample.tar.gz https://github.com/openshift-homeroom/lab-markdown-sample/archive/1.0.tar.gz
```

then unpack it into a sub directory, by running:

```execute
mkdir -p lab-sample-workshop && tar --strip-components 1 -C lab-sample-workshop -xzf /tmp/lab-markdown-sample.tar.gz
```

This should leave you with the `lab-sample-workshop` sub directory. If you were creating your own workshop, you would name this after what your own workshop is on.

Our convention is to always prefix the directory name, and thus the Git repository name where it is being hosted, with the `lab-` prefix. This way it stands out as a workshop or lab when you have a whole bunch of Git repositories on the same Git hosting service account or organisation.

With the sample workshop downloaded, change your working directory so you are in the top level directory for the workshop.

```execute
cd lab-sample-workshop
```

Run:

```execute
find .
```

to see what directories and files are included in the sample workshop.

If this was for your own workshop, you would probably now want to run:

```execute
git init
```

so you can track changes you make. Add everything into Git:

```execute
git add .
```

and commit it as the initial set of files:

```execute
git commit -m 'Initial files.'
```

We will leave it up to you to work out how to later push your workshop content up to a Git hosting service.
