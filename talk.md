<!-- .slide: data-background="lime" -->
## Collaborative support in Quaive


<!-- .slide: data-background="lime" -->
- quaive.app.onlyoffice


<!-- .slide: data-background="lime" -->
- quaive.app.libreoffice (collabora)


<!-- .slide: data-background="lime" -->
- pat-tiptap / Hocuspocus / Yjs




<!-- .slide: data-background="lime" -->
## Collaboration stories


<!-- .slide: data-background="lime" -->
- "The weekly meeting"


<!-- .slide: data-background="lime" -->
- Replaces need to send documents.


<!-- .slide: data-background="lime" -->
- Enables faster delivery when memory is still fresh.


<!-- .slide: data-background="lime" -->
- Working together on the same document.


<!-- .slide: data-background="lime" -->
- Pair programming.


<!-- .slide: data-background="lime" -->
- Collaborative whiteboard.




<!-- .slide: data-background="Yellow" -->
## About pat-tiptap


<!-- .slide: data-background="Yellow" -->
- Patternslib integration of Tiptap


<!-- .slide: data-background="Yellow" -->
- Headless / designless editor
  <br>Use your own design!


<!-- .slide: data-background="Yellow" -->
- Uses Patternslib patterns
  <br>(pat-tooltip, pat-autosubmit, etc)


<!-- .slide: data-background="Yellow" -->
- Based on ProseMirror


<!-- .slide: data-background="Yellow" -->
- Strict schema


<!-- .slide: data-background="Yellow" -->
- Potentially nice HTML


<!-- .slide: data-background="Yellow" -->
- Opinionated but well-reasoned




<!-- .slide: data-background="Blue" -->
## Tiptap as collaborative editor


<!-- .slide: data-background="Blue" -->
- Tiptap

- Yjs

- Hocuspocus


<!-- .slide: data-background="Blue" -->
### Yjs?


<!-- .slide: data-background="Blue" -->
- Conflict-free replicated data types (CRDT)


<!-- .slide: data-background="Blue" -->
- A bit like conflict resolution in ZODB (🥂 ale)


<!-- .slide: data-background="Blue" -->
- Automatic syncing


<!-- .slide: data-background="Blue" -->
- Offline support


<!-- .slide: data-background="Blue" -->
- History support


<!-- .slide: data-background="Blue" -->
- High performance


<!-- .slide: data-background="Blue" -->
## Hocuspocus


<!-- .slide: data-background="Blue" -->
- Tiptap's own collaboration backend


<!-- .slide: data-background="Blue" -->
- Websocket server


<!-- .slide: data-background="Blue" -->
- Support for databases, redis, etc 




<!-- .slide: data-background="Blue" -->
## Our implementation


<!-- .slide: data-background="Blue" -->
## DEMO




<!-- .slide: data-background="Blue" -->
## First Prototype


<!-- .slide: data-background="Blue" -->
- Shared-secret token with encoded data:
  <br>
  <br>Document UUID,
  <br>User name,
  <br>User color,


<!-- .slide: data-background="Blue" -->
- Hocuspocus decodes token.


<!-- .slide: data-background="Blue" -->
- Content from textarea.


<!-- .slide: data-background="Blue" -->
- Saves via client.


<!-- .slide: data-background="Blue" -->
## Problems? 🤷


<!-- .slide: data-background="Blue" -->
- No collaboration history.


<!-- .slide: data-background="Blue" -->
- Only initiating user can save.
  <br>(unless custom deferring view)


<!-- .slide: data-background="Blue" -->
- Permissions check only client side.
  <br>(might be sufficient)




<!-- .slide: data-background="Blue" -->
## Second prototype


<!-- .slide: data-background="Blue" -->
- Shared-secret token with encoded data:
  <br>
  <br>Document UUID,
  <br>User name,
  <br>User color,
  <br>Plone JWT authorization token,
  <br>API endpoint URL for the document.


<!-- .slide: data-background="Blue" -->
- Hocuspocus loads content
  <br>
  <br>plone.restapi ♥️


<!-- .slide: data-background="Blue" -->
- Hocuspocus checks permissions.


<!-- .slide: data-background="Blue" -->
- Hocuspocus saves deferred.


<!-- .slide: data-background="Blue" -->
## Problems? 🤷


<!-- .slide: data-background="Blue" -->
- Still no history support.


<!-- .slide: data-background="Blue" -->
- Hocuspocus needs document schema.




<!-- .slide: data-background="Blue" -->
## Third prototype


<!-- .slide: data-background="Blue" -->
- Saves the Yjs document.


<!-- .slide: data-background="Blue" -->
- Uses plone.app.textfield
  <br>
  <br>Yjs document in `raw` field.
  <br>transformed HTML in `output` field.


<!-- .slide: data-background="Blue" -->
- Document transformer could be implemented Plone-side.




<!-- .slide: data-background="Cyan" -->
## Status


<!-- .slide: data-background="Cyan" -->
- Working prototype 1 + 2 (partly).


<!-- .slide: data-background="Cyan" -->
- Expect this to be ready soon(ish).


<!-- .slide: data-background="Cyan" -->
- Need real world testing 🤷




<!-- .slide: data-background="Blue" -->
### Open questions


<!-- .slide: data-background="Blue" -->
- Bundling questions
  (mixing non-module app with module imports in a module-type node app)


<!-- .slide: data-background="Blue" -->
- Plone as storage backend? 🤷




<!-- .slide: data-background="Purple" data-background-image="./resources/imgs/thats_all_folks.svg" -->




<!-- .slide: data-background="DarkViolet" -->
## Questions
