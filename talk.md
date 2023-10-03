<!-- .slide: data-background="lime" -->
## Collaborative support in Quaive


<!-- .slide: data-background="lime" -->
- quaive.app.onlyoffice

- quaive.app.libreoffice (collabora)

- pat-tiptap / hocuspocus / yjs


<!-- .slide: data-background="lime" -->
## Collaboration stories


<!-- .slide: data-background="lime" -->
- "The weekly meeting"

- Replaces need to send documents.

- Enables faster delivery when memory is still fresh.


<!-- .slide: data-background="lime" -->
- Working together on the same document.

- Pair programming.

- Collaborative whiteboard.



<!-- .slide: data-background="Yellow" -->
## About pat-tiptap

- Patternslib integration of tiptap

- headless / designless editor

- Uses and integrates Patternslib patterns (pat-tooltip, pat-autosubmit, etc)


<!-- .slide: data-background="Yellow" -->
- Based on ProseMirror

- Strict schema

- Potentially nice HTML


<!-- .slide: data-background="Yellow" -->
- pat-tiptap is an opinionated but well-reasoned editor


<!-- .slide: data-background="Blue" -->
## tiptap as collaborative editor


<!-- .slide: data-background="Blue" -->
- tiptap

- yjs

- hocuspocus


<!-- .slide: data-background="Blue" -->
### yjs?


<!-- .slide: data-background="Blue" -->
- Conflict-free replicated data types (CRDT) framework

- A bit like conflict resolution in ZODB (ale)


<!-- .slide: data-background="Blue" -->
- automatic syncing

- offline support

- history support

- high performance


<!-- .slide: data-background="Blue" -->
## hocuspocus


<!-- .slide: data-background="Blue" -->
- tiptap's own collaboration backend

- websocket server

- support for databases, redis, etc


<!-- .slide: data-background="Blue" -->
## Our implementation


<!-- .slide: data-background="Blue" -->
## DEMO


<!-- .slide: data-background="Blue" -->
## First Prototype


<!-- .slide: data-background="Blue" -->
- shared-secret token with encoded data (document id, username, color)

- pat-tiptap init with content from textarea

- hocuspocus decodes token

- changes are saved back to Plone from the client.


<!-- .slide: data-background="Blue" -->
### Problems


<!-- .slide: data-background="Blue" -->
- no collaboration history.

- only initiating user can save
  (unless custom view queuing/deferring all requests)

- Permissions never checked server side
  (but for hijacking you'd need shared secret)


<!-- .slide: data-background="Blue" -->
### Second prototype


<!-- .slide: data-background="Blue" -->
- token plus Plone JWT authorization token and base URL of the document.

- get the document via plone.restapi.

- check document permissions.

- saves are deferred.

- document schema must be available on the server.


<!-- .slide: data-background="Blue" -->
### Third prototype


<!-- .slide: data-background="Blue" -->
- Saves the Yjs document

- Uses plone.app.textfield `raw` (Yjs) and `output` (transformed).

- Document transformer could be implemented Plone-side.


<!-- .slide: data-background="Blue" -->
### Open questions


<!-- .slide: data-background="Blue" -->
- Bundling questions
  (mixing non-module app with module imports in a module-type node app)

- Plone as storage backend?


<!-- .slide: data-background="Cyan" -->
## Status


<!-- .slide: data-background="Cyan" -->
- Working prototype 1 + 2 (partly).

- Expect this to be ready soon(ish).

- Need real world testing.


<!-- .slide: data-background="Purple" data-background-image="./resources/imgs/thats_all_folks.svg" -->


<!-- .slide: data-background="DarkViolet" -->
## Questions
