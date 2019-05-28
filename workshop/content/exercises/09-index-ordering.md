---
Title: Index Ordering
PrevPage: 08-page-navigation
NextPage: 10-presenter-slides
---

Although not usually visible by default when viewing the workshop dashboard, a page index is created for the workshop content. To view the page index, drag to the right the divider between the workshop content and the tabbed area. When the width of the workshop content is large enough, the page index will be displayed. The page index will also be visible if the workshop content is opened in a browser window of its own and the browser window width is large enough.

The top part of the page index will list those pages which are found on the top level `workshop/content` directory. Beneath these pages, there will be a section corresponding to each sub directory, with the pages in those sub directories in turn listed.

By default, the order in which pages are displayed in their respective sections, is based on the name of the file for that page. Similarly, the sections corresponding to the sub directories, are ordered base on the names of the sub directories.

To override the displayed order for pages in a section, you can add the `Sort` field to the meta data of the pages. By adding this to all pages in that section, you can control precisely the order they are displayed.

An alternative, especially for pages in sub directories, is to add a number (zero padded to the left as necessary) at the start of the name of the file for that page. To override what name is used when the page is displayed in the page index, you can set the `Title` field in the meta data of that page.

Using a number prefix can also be used for sub directories, and thus where that section is placed relative to others, but you cannot override the title used for the section and it will always be based on the name of the sub directory. Instead of dictating order by the name of the sub directory, you can instead add a file called `sort` into the sub directory, and in that add an integer value dictating it's position in the sort order.
