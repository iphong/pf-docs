# Content List

Content list is written following event-driven architecture. Room is an object which is used to store element in Content List. Each room instance contains room Id array. This array stores all element id in this room.&#x20;

Room class has 3 main functions: add, remove and listen

* add: add elementId into room
* remove: remove elementId out of room
* listen: receive event and handle it for all member of room

## Folder structure

* elements/room.ts: class Room,  handle the event in listen function
* render-root.tsx: handle when initializing  a new element
* elements/fns.ts -> createElementStore fns: undo/redo handling

#### There are some places where we need to use roomId as a selector instead of main selector for styling

* elements/index.ts:
* render-root.ts
* elements/style.ts
