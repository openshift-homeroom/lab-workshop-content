Individual module files can use either Markdown or AsciiDoc markup formats. The extension used on the file should be `.md` or `.adoc`, corresponding to which formatting markup style you want to use. The extension is though always left off when listing the module name in the YAML files used for configuration.

In conjunction with the standard Markdown and AsciiDoc, additional annotations can be applied to code blocks. The annotations are used to indicate that a user can click on the code block and have it copied to the terminal and executed, or copy the code block into the paste buffer so they can paste it to another window.

If using Markdown, to annotate a code block so that it will be copied to the terminal and executed, use:

<pre><code>```execute
echo upper
```</code></pre>

Using this, we have:

```execute
echo upper
```

When you click on the code block the command will be executed in the upper terminal.

If using AsciiDoc, you would instead use the `role` annotation in an existing code block:

<pre><code>[source,bash,role=execute]
----
echo upper
----
</code></pre>

To have a command be executed in the lower terminal, use `execute-2` instead of `execute`:

<pre><code>```execute-2
echo lower
```</code></pre>

Using this, we have:

```execute-2
echo lower
```

Note that having two terminals is an option and not the default. For this workshop two are displayed because the `Dockerfile` files set the `TERMINAL_TAB=split` environment variable. If you didn't need the terminal tab to be split and two terminal sessions shown, remove the setting for this environment variable.

In the case where you do have two terminals, if you want to be clear when a command is being executed in the upper terminal, instead of `execute`, you can use `execute-1` for the annotation on the code block.

In most cases, a command you execute would complete straight away. If you need to run a command that never returns, with the user needing to interrupt it to stop it, you can use the special string `<ctrl+c>` in the code block.

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

When the user clicks on the latter, the prior command will be interrupted.

Instead of executing a command, you wanted the content of the code block to be copied into the paste buffer, you can use:

<pre><code>```copy
echo copy
```</code></pre>

Yielding:

```copy
echo copy
```

After clicking on this code block, you could then paste the content into another window.

For AsciiDoc, similar to `execute`, you would add the `role` of `copy`:

<pre><code>[source,bash,role=copy]
----
echo copy
----
</code></pre>
