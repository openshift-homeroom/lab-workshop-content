---
Title: AsciiDoc Support
PrevPage: 11-build-and-setup
NextPage: 13-share-workshops
---

Workshop content needs be written as Markdown. There is currently no support for providing content as AsciiDoc within the structure which has been described.

Because existing workshops may have been written in AsciiDoc for a prior tool called Workshopper, a compatibility mode is provided where Workshopper can be used to render the workshop content. This should only be used for existing content and should not be used when developing new content, as future support for Workshopper is not guaranteed.

When using Workshopper compatibility mode and you want to build the content into a container image, you should replace the content of the `workshop` directory with the content used with Workshopper. By default, it is expected that the file `workshop/_workshop.yml` exists and is the file which the `WORKSHOPS_URL` environment variable would have been set to reference were Workshopper being used. The workshop modules file `_modules.yml` and any content must also reside in the `workshop` directory.

For workshop content designed for Workshopper which cannot be made to fit this structure, other options exist to be able handle it, including being able to support content hosted on a separate site. These other options will not however be described here.

As to AsciiDoc code block annotations supported by Workshopper, the `copypaste` annotation is supported. Additional annotations for `execute`, `execute-1` and `execute-2`, are also supported, with them being treated in a similar way as to how they are handled in Markdown.
