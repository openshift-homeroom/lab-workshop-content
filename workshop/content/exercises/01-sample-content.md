---
Title: Sample Content
PrevPage: ../setup
NextPage: 02-directory-layout
---

This sample workshop, as well as explaining to you how to create a workshop, is provided as a starter template you can use. You will download a copy of it, then start modifying the content and configuration to suit what you need for your workshop.

To download the sample workshop run:

```execute
curl -sL -o /tmp/workshop-content.tar.gz https://github.com/openshift-labs/workshop-content/archive/master.tar.gz
```

then unpack it into a sub directory, by running:

```execute
mkdir -p lab-sample-content && tar --strip-components 1 -C lab-sample-content -xzf /tmp/workshop-content.tar.gz
```

This should leave you with the `lab-sample-content` sub directory. If you were creating your own workshop, you would name this after what your own workshop is on.

Our convention is to always prefix the directory name, and thus the Git repository name where it is being hosted, with the `lab-` prefix. This way it stands out as a workshop or lab when you have a whole bunch of Git repositories on the same Git hosting service account or organisation.

With the sample workshop downloaded, change your working directory so you are in the top level directory for the workshop.

```execute
cd lab-sample-content
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
