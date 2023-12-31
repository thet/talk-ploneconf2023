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

The weekly meeting

8 People do a meeting. One person is doing the minutes. 3 days later, the minutes are compiled and sent around for approval. 2 days later, everybody said ok - the dutch say "pee'd on it" - and one day later the final minutes are sent around. One day before the next meeting.

Wouldn't it be nice if we all would write the minutes during the meeting, or at least in the 10 mins afterwards. Immediate compilation and approval? And then everybody knew which tasks have to be done until next weeks meeting?

Ok, let's do it that way. What tool can do that? Google docs - but everybody needs a google account. Microsoft teams? Same story. Onlyoffice or Collabora? A third system needed again. And why would we write A4, we want to be online only! Confluence has a collaborative web editor… But its atlassian and behaves interestingly. And is expensive. And a third system. We are plone users! And we use plone as an intranet. Can't we have it there?

Apropos intranet: Many content types in an intranet could be accessed in parallel, because content in an intranet is often used in meetings. Collaboratively. And each time a lock is forgotten, a doc can't get edited anymore. Annoying. When we do a meeting, we open the event type to check the agenda. Everybody with write access could write, if we had collaborative editing. Even the minutes could live in the event. Attendees could get added while others have the event open.

But also tasks on a board could be worked on in parallel.


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
HTML output. A `<img>` tag specified as a child of a `<figure>` tag but not as
child of a `<div>`? It would be stripped out. An attribute other than `href` and
`title` on a link tag? The attribute would be removed. A `<iframe>` pointing to a
resource other than Vimeo or YouTube? It would not be included. An empty
paragraph? If it is not explicitly allowed, it will be removed.

These are only examples. But the strictness of tiptap resp. Prosemirror is a
good thing. No more ugly HTML produced by copy/pasting from Word. The HTML is
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


- tiptap-collaboration-server (hocuspocus)


### First Prototype

- DEMO

- Quaive generates a token with a shared secret, encoding some data to be used on the collaboration server.

- pat-tiptap initialized with content from textarea, connects to hocuspocus using the token from Quaive

- hocuspocus tries to decode the token with the shared secret. If it works, the user is successfully authenticated.

- pat-tiptap uses pat-autosubmit to save back the changed content to the Plone instanc.


#### Problems

- Storing as plain HTML withdraws the collaboration history. This drawback is acceptable, when we only want to enable collaboration but don't need to provide a thorough history. For every new collaboration session the tiptap/yjs representation of the document would be generated from the HTML.

- If the storage is initiated client-side we need to keep track of the initiating user and only that should store back the changes to Plone. Otherwise there would be a lot of concurrent requests from different clients trying to save the same state.

- Document access permissions are never checked on the server side.


### Second prototype

- A shared secret is used to encrypt data in Plone and send it via pat-tiptap over to the hocuspocus server.

- The data includes the Plone JWT authorization token, the document UID and the base URL of the document.

- The hocuspocus server communicates with plone.restapi to retrieve the document. If the connected user would not have the rights to view it, he would not be able to connect. If the user does not have the rights to edit the document, it would be opened read-only.

- Changes are debounced and only commited back to the Plone server via plone.restapi calls after a specific time interval.

- The transformation chain on the hocuspocus server has to replicate the same extensions as used for the original document. The extensions define the allowed structure of the resulting HTML. Basically it has to use the same extensions as pat-tiptap on the client.


### Third prototype

- Same as second, but:

- We use plone.app.textfied to store the history aware yjs data structure. The yjs document is stored in plone.app.textfield's `raw` field and the transformed representation in the `output` field. This way we preserve the history and are able to restore it on a completly new collaboration session.



### Open questions


- How can we use pat-tiptap in the hocuspocus node application? Currently,
  without any bundler, we have to define the hocuspocus backend as
  `type=module`, so that we can use ES6 imports. For `pat-tiptap` we cannot
  define it as `type=module` and thus we cannot directly import files in
  hocuspocus...

- Is Plone ready to serve as backend for a collaboration editor? Or would be a high-performance store like redis better suited?




