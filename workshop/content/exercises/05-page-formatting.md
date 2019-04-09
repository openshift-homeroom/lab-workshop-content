---
Title: Page Formatting
PrevPage: 04-workshop-config
NextPage: 06-data-variables
---

As you have gone through this workshop, you have seen how you have been guided from one topic to the next.

The starting point for the workshop was the page `workshop/content/index.md`. This is the home page.

The markup format used in pages is Markdown, specifically the [GitHub flavored Markdown](https://github.github.com/gfm/).

In addition to the content of the page, each page contains a header providing metadata about the page.

```
---
Sort: 1
Title: Workshop Overview
NextPage: setup
ExitSign: Setup Environment
---
```

This is where you set the title for the page, and provide details about how the pages link together to provide a navigation path for the workshop. Details about defining the navigation path are covered later, as is overriding sorting for how pages are listed in the page index.

On top of the standard Markdown, a number of extensions are implemented. These are annotations you can apply to code blocks so that a user can click on the code block and have it copied to the terminal and executed, or copy the code block into the paste buffer so you can paste it to another window.

To annotate a code so that it will be copied to the terminal and executed, use:

<pre><code>```execute
echo upper
```</code></pre>

Using this, we have:

```execute
echo upper
```

When you click on the code block the command will be executed in the upper terminal.

To have a command be executed in the lower terminal, use:

<pre><code>```execute-2
echo upper
```</code></pre>

Using this, we have:

```execute-2
echo lower
```

Note that having two terminals is an option and not the default. For this workshop two are displayed because the `Dockerfile` and `.s2i/environment` files include `TERMINAL_TAB=split` environment variable. If you didn't need the terminal tab to be split and two terminal sessions show, remove the setting for this environment variable.

In the case where you do have two terminals, if you want to be clear when a command is being executed in the upper terminal, instead of `execute`, you can use `execute-1` for the annotation on the code block.

In most cases, a command you execute would complete straight away. If you need to run a command that never returns, with the user needing to interrupt it to stop it, you can use the value `<ctrl+c>` in the code block.

<pre><code>```execute
&lt;ctrl+c&gt;
```</code></pre>

You could then have:

```execute
sleep 3600
```

followed by:

```execute
<ctrl+c>
```

Instead of executing a command, if you instead wanted to content of the code block to be copied into the paste buffer, you can use:

<pre><code>```copy
echo copy
```</code></pre>

You could then paste this into another window.
