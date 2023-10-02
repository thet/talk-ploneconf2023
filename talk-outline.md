Collaboration revolutions in Quaive.


- pat-tiptap
- quaive.app.collabora
- collective.xxx
- collective.tiptap


-> - plone.app.tinymce





# Collaboration revolutions in Quaive

## Collaborative support in Quaive

- tiptap / hocuspocus / yjs
- quaive.app.libreoffice (collabora)


## Use cases



## Collabora integration



## tiptap - collaborative editor


### pat-tiptap

about the tiptap editor I have already given a talk at the - online-only - Plone Conference 2021.

tiptap is a headless JavaScript editor which is based on Prosemirror. That translates to:

headless: tiptap comes with no design in place. You have to build the UI - all
the buttons, overlays, labels, etc - yourself. This is actually a good thing -
you're not bound to the editors design system which very likely does not
resemble what you - or your designer - would have built yourself. In Quaive we
integrate the editor in a way that it perfectly fits into the rest of the
application. We also have the toolbar separated from the editor itself which is
most often not a natural feature of editors like TinyMCE.

Speaking of TinyMCE, the second "feature" of tiptap is that it is based on the
Prosemirror editor. Unlike TinyMCE, which allows basically for almost any kind
of HTML structure in the content Prosemirror is very strict. You have to define
the schema and only what the schema permits will be allowed in the resulting
HTML output. A <img> tag specified as a child of a <figure> tag but not as
child of a <div>? It would be stripped out. An attribute other than `href` and
`title` on a link tag? The attribute would be removed. A <iframe> pointing to a
resource other than Vimeo or YouTube? It would not be included. An empty
paragraph? If it is not explicitly allowed, it will be removed.

These are only examples. But the strictness of tiptap resp. Prosemirror is a
good thing. No more ugly HTML produces by copy/pasting from Word. The HTML is
always as clean as you have defined it.

We have created the `pat-tiptap` Patternslib addon which has a lot of
opinionated but well-reasoned configuration already done. pat-tiptap is still
very flexible and could probably just replace the editor in your web
application. Also it is open source and contributions are very welcomed - but
be warned, for Patternslib every configuration change will pass a specification
phase with our Designer to keep everything as clean as possible. But that
should not prevent anyone from contributing. The extra review/specification
phase is a good opportunity to get qualified feedback.

### yjs

And now to the collaboration part. tiptap has integrated the yjs shared editing
framework. yjs is a framework providing "CRDT" types, Conflict-free replicated
data types. This allows for datatypes to sync automatically over the web, have
offline support, have granular versions with the ability to travel back in time
and it prevents any conflicts when syncing the data with other clients.

https://yjs.dev/#features
https://github.com/yjs/yjs
https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type


https://github.com/Patternslib/tiptap-collaboration-server/blob/main/src/tiptap-collaboration-server.js
https://github.com/Patternslib/pat-tiptap/pull/6


## our implementation

- pat-tiptap 


- tiptap-collaboration-server


### First Prototype

- tiptap retrieves the content from the textarea in the client
- tiptap saves back the content with pat-autosubmit

### Second prototype

- A shared secret is used to encrypt data in Plone and send it via pat-tiptap
  over to the hocuspocus server.

- The data includes the Plone JWT authorization token, the document UID and the
  base URL of the document.

- The hocuspocus server communicates with plone.restapi to retrieve the
  document. If the connected user would not have the rights to view it, he
  would not be able to connect. If the user does not have the rights to edit
  the document, it would be opened read-only.

- Changes are debounced and only commited back to the Plone server vie
  plone.restapi calls after a specific time intervar.

- We use plone.app.textfied to store the JSON structure in the `raw` field and
  a transformed document in the `output` field.

- The transformation chain on the hocuspocus server has to replicate the same
  extensions as used for the original document. Basically it has to use the
  same extensions as pat-tiptap.



### Open questions

- How can we use pat-tiptap in the hocuspocus node application? Currently,
  without any bundler, we have to define the hocuspocus backend as
  `type=module`, so that we can use ES6 imports. For `pat-tiptap` we cannot
  define it as `type=module` and thus we cannot directly import files in
  hocuspocus...

- Is Plone ready to serve as backend for a collaboration editor?

- 


